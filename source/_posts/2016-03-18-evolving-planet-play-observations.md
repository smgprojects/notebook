---
layout: post
title: "Evolving Planet Play Observations"
date: 2016-03-18 10:51
tags: [archaeogaming]
categories:
- Observations
...

* Table of Contents
{:toc}

# main conceit
Android & IOS. Game website is at [http://www.evolvingplanetgame.com/](http://www.evolvingplanetgame.com/). Main blurb:

>It's the year 3016, and you are in charge of an archaeological expedition to the planet Kepler-1138. Your aim is to know what happened to the Lovans, humanoid aliens that became extinct for unknown reasons. <br> You will use artificial life to replicate the story of the mysterious species. Will you develop their technology, make them experts on warfare or strengthen their cultural influence? Choose carefully your strategy to reveal the past of the Lovans, and also their future.

- So an agent based model. Game play revolve around tweaking settings in order to guide the bots across the planet.
- framed explicitly as 'xenoarchaeology'
- evolution of the robots artificial society then is examined for clues on the 'actual' society of Lovans

# tutorial levels
- framing discussion for each level mimics evolution of hominins on earth - dispersal, colonisation of new ecological niches, ect.
- eg Level 5:

  > Our bots will need to interact with other groups during the archaeological expedition. <br> The planet was not populated only by Lovans, just like the Earth was not a Homo sapiens-only club. We shared Eurasia with Neanderthals for 5,000 years. They were also hominis quite similar to us in many respects, including the use of technology, culture and even language. <br> The Neandeerthals disappeared as a specides over 30,000 years ago. However, our DNA says that each of us has a little bit of Neeanderthal inside. And trust me, DNA never lies!

- These blurbs are framed as a discussion with your (junior, woman) colleague, Dr. Lovelace. <- I think that's the name. I neglected to write it down and I don't want to go back to level 1. Nod to computing history, but replicates power dynamics of 21st century archaeology (unwittingly?) Lovelace is there at the planet first, you the emminent professor appear on the scene. I need to go back [and check if the player character is male](#todo:20).
- Art work between the levels seems to imply that the bots are not aware that they are bots, that they are sentient, have culture, and wonder why the hell they're doing these different things.
- Art work seems to reproduce some of the tropes of museum dioramas - mostly naked 'cave people', men armed, women looking on... but [I need to replay that level](#todo:0) (I think it was between 3 & 4 that I saw that art work.

# game play
- you're presented with a map of the planet. Topography is represented; vegetation, slope, aspect etc all have an effect on how the bots move.
- configure the bots to meet the targets; targets have to be reached via particular times (denoted by a time bar; optimal times to hit your targets are coloured blue to white). Targets literally are places on the ground that the bots have to reach. If I could figure out [how to take a screenshot on my damned tablet, I would](#todo:40).
- Bots have 'evolution points' which tally up the longer the bots live; you get a set amount when you start playing. They can be spent on mobility, reproduction, and technology. There are power-ups and boosts, but I'm not yet [clear on how they work](#todo:30).
- A population graph keeps track of how well your bots are doing. They all die: mission is a failure and we haven't learned how the Lovans managed this particular task.
- Other populations of bots are simulated; you can't control them. But trouble ensues when your Lovans intersect with them. You know they're bad, because they'r coloured red.

# initial thoughts
- We make ABM in archaeology to simulate our understanding of how particular processes worked in the past. When the results of the simulation match the archaeology on the ground, we say we now have a good working model of process x. Or at least, that's how it ought to work - too often we say we're actually simulating x, rather than our just-so story of x. ABM per me is for testing our stories about the past, to get a range of possible behaviours, that allow us to explore and discount competing ideas - see [Graham & Weingart](http://www.scottbot.net/HIAL/wp-content/uploads/2011/11/Preprint-Graham-and-Weingart.pdf)
- this game does a good job of framing a narrative around what seems to be a basic [rabbits-grass model](http://ccl.northwestern.edu/netlogo/models/RabbitsGrassWeeds), although it does have direction in it - ie, the player messes not just with the global population parameters (as is done in many ABM) but with the actual goal-setting of the agents in terms of their interaction with the environment
- which brings up the interesting side effect that the act of making this ABM playable inadvertently (?) turns 'evolving planet' into 'intelligent design' (ugh.)
