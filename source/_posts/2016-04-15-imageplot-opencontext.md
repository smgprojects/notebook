---
layout: post
title: "Imageplot and Opencontext"
date: 2016-04-15 11:47
tags: [archaeology, how-to, images]
categories:
- Meta
...

* Table of Contents
{:toc}

# Get data out of Open Context

+ Eric on how to get stuff out of OpenContext:

[https://twitter.com/ekansa/status/720706858093137920](https://twitter.com/ekansa/status/720706858093137920)

[https://twitter.com/ekansa/status/720827996915900416](https://twitter.com/ekansa/status/720827996915900416)

```
http://opencontext.org/media-search/Turkey.json?proj=22-kenan-tepe&prop=22-image-type---22-field-photo&response=uri-meta
```

+ note the `.json?` location. Copied the results into Excel & filtered by thumbnail. It was just easier.
+ put the URLs into a text file
+ used wget: `wget -r --no-parent -w 2 --limit-rate=10k -i input.txt -nH -nd -np`
+ this puts the images into a single folder, rather than replicating opencontext's deep folders

# Analyze images with imageplot

+ in imageplot, open imagemeasure.txt from the extras folder, run it.
+ in imageplot, open imageplot.txt and run that.
+ for 3d viz of hue, saturation, brightness, see Joel's post.

![img](https://pbs.twimg.com/media/CgFTo6yUUAAjsaR.jpg) [https://twitter.com/electricarchaeo/status/720949378526113792](https://twitter.com/electricarchaeo/status/720949378526113792)

![img](https://pbs.twimg.com/media/CgFWG0mVIAAUA19.jpg) [https://twitter.com/electricarchaeo/status/720952091364233221](https://twitter.com/electricarchaeo/status/720952091364233221)
