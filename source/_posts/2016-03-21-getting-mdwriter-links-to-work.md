---
layout: post
title: "getting mdwriter links to work"
date: 2016-03-21 15:06
tags: [notebook]
categories:
- Meta
...

* Table of Contents
{:toc}

A useful add-on for Atom is [md-writer](https://atom.io/packages/markdown-writer). In particular, it allows me to make internal links to other notes in my notebook by highlighting a term, then hitting `command+shift+k`. (This brings up a menu to allow me to select the relevant note. Say I wanted to cross-link to the code I used to sonify [the topic model][c0d5437a] of John Adams' diaries, I'd highlight the term, hit the keystrokes, and there we go. Seems a little thing, but it's very important for turning this whole thing into a wiki-style notebook.

Once you've installed the package, you need to set up a `.cson` file for markdown that tells it where to find the posts. For reference sake, it should look something [like this](https://github.com/zhuochun/zhuochun.github.io/blob/cb34e3c16d42c52b281c34920ad55bbca223ac23/_mdwriter.cson). The important bits there are these:

```
siteUrl: "http://smgrojects.github.io/"
# URLs to tags/posts/categories JSON file
urlForTags: "http://smgrojects.github.io/tags.json"
urlForPosts: "http://smgrojects.github.io/posts.json"
urlForCategories: "http://smgrojects.github.io/categories.json"
```

Those .json files are generated from [this code](https://gist.github.com/zhuochun/fe127356bcf8c07ae1fb); they live inside my `source` folder and are generated when I `jekyll build`.

  [c0d5437a]: http://smgprojects.github.io/sonification-of-john-adams/ "sonification of john adams"
