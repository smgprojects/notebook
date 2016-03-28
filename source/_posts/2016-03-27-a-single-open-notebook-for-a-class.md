---
layout: post
title: "a single open notebook for a class?"
date: 2016-03-25 09:07
tags: [teaching, archaeogaming]
categories:
- Meta
...

* Table of Contents
{:toc}

What if I set up this open notebook infrastructure as a communal notebook for an entire class? How could that work? Maybe by making the hidden drafts folder (which I normally write into with `rake draft`) its own github repo. Students would fork it, then put their notes into it. I'd sync from that, then fold into the overall structure & push live to the net.

## Problems
- getting students to observe YAML conventions automatically. Having a template is great, but everyone keeps overwriting the damned thing causing conflicts. SOLUTION: a rake file?
  - which opens another problem, windows vs mac etc.
- more problems would emerge, no doubt

## How to test this?
- Maybe with Andrew R, set something similar up for our No Man's Sky stuff?
