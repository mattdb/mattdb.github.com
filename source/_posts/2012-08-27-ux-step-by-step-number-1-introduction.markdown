---
layout: post
title: "UX Step by Step #1: Introduction"
date: 2012-08-27 15:40
comments: true
categories: [UX, Brewtime]
---

This is post #1 of a [multi-post series](/blog/categories/brewtime/) about the interface design and construction of a sample application. I'll be demonstrating some of my thought processes, decisions I make, and problems I may encounter. We'll be focusing both on the user interface design and the interesting parts of actually building the app to implement the design. Come along for the ride.


## Mission statement


First step is obviously knowing what you want to build. It's always a good idea to have a "Mission Statement" for any project-- a quick, 3 sentence max (1 or 2 would be better) statement that is the root of what your application does.

I've been getting in to homebrewing recently, so let's go there for some useless but still fun material. I've got plenty of software to help me formulate exactly what is going in to each brew, but I've found it hard to keep track/remember of when different stages of the beer are nearing completion (or, overdue, maybe). Fermentations typically go anywhere from 1-4 weeks, and then there's various additional stages you may want to do afterwards (secondary fermentation, dry hopping, bulk aging, to name a few). There's typically a range for the end of the stage-- you need to check in on your beer during that time even more to see when it's ready for the next step.

So, here we go, mission statement time:

> Provide a concise summary of the different brews a brewer currently has going. The brewer should be able to determine at a glance what needs watching (might be done), what's probably overdue, and what can be safely ignored for the time being.

Come on inside for the rest of the app's conception, with pictures!

<!-- more -->

## Sketching our primary view

OK, so we're clearly going to want to show a list of brews that are currently going on. Let's make it visual, though-- pure text (i.e. "OVERDUE", "Done in 3-10 days" etc) wouldn't really communicate very efficiently, nor would it be effective in easily showing the brewer what truly should have his attention first. We want a cohesive display that really shows us visually how everything relates to each other, and especially to time.

Time to break out a sketchpad. Here's my initial sketch, using a Gantt chart as a rough inspiration:

{% img /images/brewtime/sketch.png %}

The big vertical line representing "Today", each row representing a brew in process, and each pill-shaped "capsule" representing a brewing step. And a little bit of beer nerd humor for good measure. We can also see some of the uncertainties I'm facing here:

- How to represent the "fuzziness" of the end of each brewing step: I want to be able to display the time period towards the end of the step that we think it's possible it could be done.
- How to clearly display "past due", "any day now", "not yet" statuses (semi-related to above) 
- Colors: these went in as I went, and we can already see some conflicts
- Future: Both in the first line (the reddish "Lager" step) and the final line with it's "Planning?" represent some problems with future predictions

Let's tackle these individually:

### Fuzziness

I like the "end capsule" design I started using in lines #3 and 4, but as drawn I'm not sure how to integrate into something like line #1-- is that an "end capsule", or a whole separate stage? Things could get cluttered quickly.

### Current status for a line

I started with the green/red capsules towards the end but this doesn't seem to fit entirely, especially the red "extended" capsule on the overdue second-to-last line. I also tried some exclamation marks on line #2, but I'm not feeling entirely happy with this either.

### Colors

As is, the "dry hop" step of line #1 and the "could be ready" end capsule of line #3 are too similar. Also, it's worth noting that we shouldn't rely entirely on color to communicate information to accommodate those who might be colorblind. Luckily we're OK on that front because the horizontal position also effectively communicates that information, the color just highlights and draws attention to the current statuses.

### Future

How do we want to display things in the future? Do we want to be able to see a general gist of what's eventually coming (we typically know what steps a particular beer is going to go through, just not exactly how long each step will be)? This could be complicated because each step typically has a variable amount of time it could take, and therefore future steps start having variable starting times, compounded by however many steps are coming before it. This seems like an additional complication(s) we could do without for now. Let's table this, and we could potentially look at this once we're further along (I'm thinking more "ghosted" capsules with our best guess for each stage to at least give a rough idea).

## Sketch, refined

With some of the issues we gathered from our first take, let's try again:

{% img /images/brewtime/sketch2.png %}

We've alleviated most of the problems from above. Highlights for the end capsules of overdue (orange) or "any day now" (green) stages draw your attention, whereas a stage that's currently active but hasn't yet hit the "ending window" will just display its end capsule as a little more saturated, or darker, or something (as I clearly noted!).

We can also keep previously completed stages fairly clean because we'll know exactly when they were completed, so no need for end capsules (or "ending windows") there. 

I also more explicitly drew the scrolling area because I wanted to display that I wanted the line labels (name of the brew) outside of it, so it can be immediately clear which brew is which no matter where the view is scrolled to.

I'm fairly happy with this as a starting point. One minor alteration I think I'll do once we're implementing is to remove the black border between a currently active stage and its ending window. This will help make it especially clear that the end capsules are not separate stages, but are just a part of the bigger stage. Also it might make sense for the rounded corners to actually go the other way on the end capsule, to better indicate that it represents the potential ending of the stage. So a currently active stage would represented like this:

{% img /images/brewtime/sketch3.png %}

Or maybe we'll end up reversing the colors, so the darker part is what we know will happen and the light part is the possible additional time. The great part about sass and representing these with css is this'll be really easy to play around with as we're building them.

## Up next

Next time, we'll be looking at setting up the basic app and getting a basic data structure laid out. Stay tuned.
