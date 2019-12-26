NPM (Node Package Manager) is great. It's easy to use, easy to configure, easy to publish packages, doesn't suffer from the age-old issue of dependency hell. It's easily one of the top 5 greatest contributions to the JS (JavaScript) ecosystem. Drawing on 7 years of experience authoring, maintaining, contributing to OSS projects in the JS ecosystem; I'll attempt to share some strategies, tools, and tips I've developed to make the process of developing OSS (Open Source Software) projects suck less.

This is the first installment in a series about developing NPM packages from an OSS maintainer perspective.

## Intro

NPM packages have a problem. It's so easy to unintentionally bloat `node_modules` that this issue has inspired its own category of memes.

**Exhibit A**

![Node modules weigh as much as a black hole](http://content.evanplaice.com/thoughts/images/nodeblackhole.jpeg)

It's time to put `node_modules` on a diet.

## First Principles

Developing OSS libraries is an immensely powerful skill to have. The ability to publish code to the wider ecosystem has a lot of benefits. Projects that reach a critical mass of users are exponentially more valuable than those that don't. More eyes leads to fewer bugs. More users means battle-tested usability. Popularity attracts maintainers which is the only effective way to guarantee the long-term sustainability of the project.

With that said, only ~5% of developers in the JS ecosystem will ever publish a package. Let's say you've broken through the initial high barrier-of-entry.

**You have:**

- learning the hairy ins-and-outs of Git
- gained sufficient familiarity with GitHub
- come up with a good idea that doesn't already exist on NPM
- found a name for your project that doesn't suck
- developed a usable MVI (Minimum Viable Implementation)
- written enough documentation for users to get a start
- filed issues for desired features and known bugs

*...phew, that's a lot*

It's time to ditch `git clone` and dust off that `npm publish` hotness.

## You've Won The First Battle

*...but the war has just begun*

Depending on your level of commitment thus far, your repository may include `[source, docs, tests, examples, demos, config, dist, license]`. 90% of which is completely unnecessary to a production-ready package. But, who cares about optimization? It has been a slog to get this far; so you pull the trigger and `npm publish` 1.0 (or 0.0.1 depending on your SemVer preferences).

![That wasn't very cash money of you](http://content.evanplaice.com/thoughts/images/wasntcashmoney.jpg)

The reality is, a significant majority of packages only ever make it this far. Compared to overall stability, usability, capability; optimization is a low-priority task. Unlike most common tasks that include an endless variety of automation tools, nothing exists to identify and grade the amount of bloat a NPM package contains<sup>1</sup>.

*<sup>1</sup> This would be a great addition to the GitHub/NPM ecosystem*

## Being a Good NPM Citizen

*Enough with the wind up*

There are 2 strategies to control what gets included in a NPM package.

### Strategy 1: The Inclusion Strategy

In `package.json` there are two options `files` and `directories`.

Usage is pretty straight-forward:

- `files` should contain an array of files/directories to include 
- `directories` should contain a list of directories to include.

**Documentation: [npm-package.json - files][]**

*`package.json`*
```json
{
  "files": [
    "filename.js",
    "directory/",
    "glob/*.{js,json}"
  ]
}
```

*Source: [Yarn package.json Documentation][]*

**Documentation: [npm-package.json - directories][]**

*`package.json`*
```json
{
  "directories": {
    "bin":"./bin",
    "doc":"./doc",
    "lib":"./lib",
    "man":"./man"
  }
}
```

*Source: [NPM's package.json][]*

### Strategy 2: The Exclusion Strategy (Preferred)

If you're already familiar with `.gitignore`, `.npmignore` operates the same way but the list applies specifically to your NPM package output.

**Documentation: [npm-package.json - npmignore][]**

*`.npmignore`*
```
.circleci/
assets/
demo/
rollup.config.js
```

## Optimization Workflow

Awesome, you have tools to optimize the package output but how do you view the package contents.

Packaging is a pretty straight-forward process. It collects the relevant files, creates a `tar` archive, then compresses it as a single `gzip` file. There are a few ways to fetch/generate this file.

### Strategy 1: Download a Published Package (Not Recommended)

You could download an existing package directly from NPM.

```sh
npm pack [package]
```

That will download a `.tgz` file that will extract by default into a folder named `package`.

### Strategy 2: Create a Dry-Run of the Package (Manual Approach)

From the root of your project run.

```sh
npm pack
```

This will create the same `.tgz` file, but locally. This is a start but fine-tuning a package will likely require downloading, extracting, and deleting the contents of the package many times.

### Strategy 3: Automate the Process (Recommended)

We know there are 3 parts to this process.

1. Creating the package
2. Extracting the package
3. Cleaning up the package

*`package.sh`*
```sh
# step 1:
npm pack

# step 2:
tar -xf [package-name]

# step 3:
rm -rf ./package
```

We don't want to delete the package contents until we're done working with it. Why not leave it as-is and just ensure it doesn't end up in either the package or the Git repo.

*`.gitignore`*
```
package/
*.tgz*
```

*`.npmignore`*
```
package/
*.tgz*
```

Then rearrange **step 3** so it happens first, and make it a npm script so it's easy to repeat.

*`package.json`*
```json
{
  scripts: {
    "package": "rm -rf ./package && npm pack | tail -n 1 | xargs tar -xf"
  }
}
```

This includes a bit of *nix magic:

- it clears the existing contents of the 'package' directory
- `npm pack` creates the `.tgz` file
- `tail -n 1` grabs the last line of the output from `npm pack` which contains the filename of the archive
- `xargs tar -xf` feeds that string into `tar` with the correct flags to extract the package

We know from before that the file will be placed in a 'package' directory. If you open that directory, you'll see the contents that will be published to NPM.

## Bonus: Want to Contribute to OSS?

Over the years I've heard the same question repeated over and over, "How do I start contributing to Open Source?" The 'easy' answer is, "contribute documentation updates." They're low risk, easy to review, and always needed.

*...but what if you hate writing documentation?*

Remember what I said about most published packages being sorely in need of optimization? Well, now you have the tools necessary to make a meaningful contribution.

Here's How:

1. The Pitch - Create a new issue outlining your intent so the maintainers are aware
2. Communicate - Start a dialog outlining what the maintainers want included in the package
3. Do Work:
  - fork the project
  - clone your fork
  - create a feature branch
  - use the tools above
  - push the changes to your fork
  - create a PR referencing the original issue
4. Revise - this may or may not require a few revisions

If you manage to get your first PR landed, congrats. This is a much more meaningful and useful start to contributing to OSS. Not only will you gain valuable experience but working through a complete review cycle is the perfect first step to becoming a regular contributor. If you feel motivated to keep working on the project, just ask how else you can help. Good contributors are always in need and hard to find.

*ProTip: Keep in mind that not all OSS maintainers regularly work on their projects. If you don't feel like waiting weeks/months to land your first PR, take a look at when the last commit was made. Some projects are always active. Some projects are updated in infrequent bursts. Most projects become abandoned either because the codebase is stable or because the maintainer lost interest/motivation in contributing. YMMV (Your Mileage May Vary).*

[npm-package.json - files]: https://docs.npmjs.com/files/package.json#files
[npm-package.json - directories]: https://docs.npmjs.com/files/package.json#directories
[Yarn package.json Documentation]: https://yarnpkg.com/lang/en/docs/package-json/#toc-files
[NPM's package.json]: https://registry.npmjs.org/npm/latest
[npm-package.json - npmignore]: https://docs.npmjs.com/misc/developers#keeping-files-out-of-your-package