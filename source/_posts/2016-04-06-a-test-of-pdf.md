---
layout: post
title: "a test of pdf"
date: 2016-04-06 19:29
tags: [workflow, notebook]
categories:
- Meta
...

* Table of Contents
{:toc}

# Boogie Board syncing

I was given a [boogie board sync](https://myboogieboard.com/ewriters/sync). It's an interesting little piece of kit, especially if you're like me you find yourself scribbling notes and reminders and so on onto available pieces of paper. It saves your scrawls as pdf, which then sync via bluetooth onto your machine (it does lots of other things too). There is an app for your phone which does all this, and evernote is also a possible destination.

I use a simple command to convert the pdfs to pngs to put into my notebook.
```
for i in *.pdf; do sips -s format png $i --out $i.png;done
```

The result:

![img](/images/test.pdf.png)
