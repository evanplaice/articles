---
title: Ship Like a Pro - Part II
published: false
description: This article covers versioning strategies for publishing packages
tags: tutorial, npm, publishing
cover_image: https://thepracticaldev.s3.amazonaws.com/i/i2hosdz0u6ux6sf1jjhx.jpg
series: ship-like-a-pro
---

# Versioning Strategies

<!-- add a quote here -->

When it comes to versioning NPM packages there is only one sensible choice, [SemVer][]

[SemVer]: http://article

## What is SemVer?

Semantic versioning, otherwise known as SemVer uses a number triplet `[major].[minor].[patch]` to represent software version numbers.

An easier way to determine which should be used is to go by the pattern...

```[breaking].[feature].[fix]```

When a dev says the version is 'bumped', that just means a new version was published.

### Major/Breaking

Breaking changes are changes that modify the existing API in a way that it'll break existing code.

**So what's an API?**

As with most things in programming, the answer is 'it depends'. Specifically, how do users interact with the codebase.

- a library's API is the functions, classes, etc that get called on
- a CLI's API are the commands that get called from the command line
- a backend's API is the REST/GraphQL endpoints
- an application's API could be the way plugins interact with the runtime

In short. If you change the code that others depend on, requiring them to rewrite the way they call your code; it's a breaking change.

**When should you bump the major version?**

Ideally, never. But if you have to, try to publish breaking versions as infrequently as possible. Save up and release all breaking changes as one big release.

### Minor/Feature

This is pretty self-explanatory. Did you add a new capability to the code base that the users are going to consume. Then you added a feature and the minor version should be bump.

### Patch/Fix

Everything else falls into this category. Add tests? Bump the patch version. Update documentation Bump the patch version. Fix a bug? Bump the patch version. Etc...

If software versioning were a clock. Major would be hours, minor would be minutes, patch would be seconds. They should be incremented at relatively the same rate.

## Practical Application

So... now that I've written the 10,000th article on SemVer ::pats self on back:: how can this information be put to use.

For starters, the version number is marked in `package.json`. So the most obvious answer is to open up this file, change the version, and run `npm publish` from the command line to publish the new version.

There are a few issues with this approach

- only NPM is aware of which commit the version was applied
- there is no release marker on GitHub (or whatever platform you use)
- the code being published hasn't been tested
- the process is manual, manual procedures are prone to human error


## Conclusion

The step most first-time Authors worry about the most is also the least significant. The less time you waste on this, the more time you'll have to dedicate to value-add work. Writing documentation, building demos, promoting projects.

And always remember, La Onda don't shine shoes.