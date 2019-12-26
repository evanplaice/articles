---
title: Ship Like a Pro - Part I
published: true
description: This article covers naming strategies for publishing packages
tags: tutorial, npm, publishing
cover_image: https://thepracticaldev.s3.amazonaws.com/i/i2hosdz0u6ux6sf1jjhx.jpg
series: ship-like-a-pro
---

# Selecting a Name

>"There are two hard things in computer science: cache invalidation, naming things, and off-by-one errors."
>
> - Martin Fowler

All jokes aside. Naming things can be a major pain. It can be hard to nail that balance of what's original, memorable, and available.

## What About JavaScript?

Why do JavaScript and Java share similar names even though they're fundamentally different languages?

Good question... Originally, developed under the name Mocha. Renamed to LiveScript during beta. Then, renamed again to JavaScript during the official first release. The reason is a lot more nonsensical than you'd expect.

JavaScript is named JavaScript to piggyback onto the hype surrounding Java's skyrocketing popularity back in 1995. Yes, really. That's where the most popular programming language in the world got its name.

## Is That Really a Viable Strategy?

Yes, and no. I gave [jquery-csv][] it's name to piggyback on the jQuery hype back in 2011. And... it worked.

Unfortunately, what was once a benefit is now a drawback. It doesn't matter that it's RFC compliant, the fastest CSV parser in the JS, and that it doesn't even really depend on jQuery. It might as well be named 'legacy-csv' because the ecosystem has moved on from jQuery.

I have since done a full rewrite named [csv-es][] but there's no guarantee that the new lib will ever share the prominence of it's predecessor.

Given a do-over, I would have picked a more original name.

[jquery-csv]: https://www.npmjs.com/package/jquery-csv
[csv-es]: https://www.npmjs.com/package/csv-es

## So, What Name Should You Use?

Honestly, it doesn't matter. A name alone doesn't make a successful project. 

Things that will make a project successful

- clear and understandable documentation
- demos outlining every feature/capability
- promoting the project on social media
- suggesting it in relevant [StackOverflow][] answers
- publishing articles showing how to use it
- giving presentations demonstrating its benefits

Really, what makes a project (even Open Source projects) successful is usable demos, good quality documentation, and better marketing.

[StackOverflow]: https://stackoverflow.com/

## Now What?

Don't get stuck obsessing over the name

If you're really struggling

1. Write down 10 different names that could work
1. Wait a day
1. Look at the names again
1. Pick the one you like best

If that fails, rinse and repeat.

## The Hard Part

Is the name available? Go to [npmjs.com][] and search for it

Chances are, it's probably already taken. Not only is it taken but every viable variation of it is also taken.

If one of the names is being squatted on (ie dead GitHub link), you could try [filing a dispute][] with NPM.

Or! Like I said previously the name doesn't matter as long as it's original, memorable, and available.

So, open a thesaurus, use the Latin equivalent, create a [portmanteau][], play Ouija; do whatever it takes to unblock your creativity an pick the thing so you can move on.

[npmjs.com]: https://www.npmjs.com/
[filing a dispute]: https://docs.npmjs.com/misc/disputes.html
[portmanteau]: https://en.wikipedia.org/wiki/Portmanteau

## Conclusion

The step most first-time Authors worry about the most is also the least significant. The less time you waste on this, the more time you'll have to dedicate to value-add work. Writing documentation, building demos, promoting projects.

And always remember, La Onda don't shine shoes.