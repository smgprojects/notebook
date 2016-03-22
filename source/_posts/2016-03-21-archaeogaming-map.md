---
layout: post
title: "archaeogaming map"
date: 2016-03-21 20:49
tags: [archaeogaming]
categories:
- Observations
...

* Table of Contents
{:toc}

A while back Andrew Reinhard devised a map of questions / relationships that could be usefully filed under the 'archaeogaming' rubric. I think it'd be handy to have a copy of that map filed here. The writeup of how I made it is on [the blog](http://electricarchaeology.ca/2015/12/18/a-map-of-archaeogaming/)

![archaeomap](images/archaeomap.jpg)

```
###
URL <- paste0(
  "https://gist.githubusercontent.com/shawngraham/2bfad0c10e7519a630a9/raw/",
  "7a7a2da8c4358a81e0dc05cc64405d7c9f975803/archaeomap-flare.json")

## Convert to list format
Flare <- jsonlite::fromJSON(URL, simplifyDataFrame = FALSE)

# Use subset of data for more readable diagram

radialNetwork(List = Flare, fontSize = 10, opacity = 0.9)
diagonalNetwork(List = Flare, fontSize = 10, fontFamily = "xkcd", opacity = 0.9, width = 500)

```
