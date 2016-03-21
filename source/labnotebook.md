---
layout: page
title: How the Notebook Works
permalink: /notebook/
---

## About This Notebook

This notebook is a fork of [Jason Heppler's](http://notebook.jasonheppler.org/). I excerpt his original 'about' page below, as I am going to follow his model, which "is built on top of Github using Jekyll, a static site generator built by Tom Preston-Warner and others in the open source community." It allows:

- The ability to write offline in Markdown, but publish the material in any format [needed].
- An ability to host the production version of the notebook on the web, open for anyone to read and reference.
- A way to easily embed bibliographic references.
- The ability to link to articles and posts within the notebook with persistent URLs and bibliographic references, since the notebook is a record of work before it appears in publication elsewhere.
- The ability to render software code in a pleasing manner.

I'll just note here that I have a script on my machine that turns my annotations on pdfs into a single markdown document; another script makes URLs to open the original annotation on the appropriate page within Skim - see [Exporting your annotations from Skim](http://electricarchaeology.ca/2015/06/28/exporting-your-pdf-annotations-from-skim/) and [Custom Skim URLs](http://www.dansheffler.com/blog/2014-07-02-custom-skim-urls/). So in any of my notes if you see a link to a page number, that opens a pdf at the right spot on my machine.

I've also added the ability for readers to leave annotations on any part of this notebook using the [hypothesis](https://hypothes.is/) web annotation architecture. See that strip down the right hand side of the page? Click on there to get started!

## Notes, Essays, Categories, Tags

*Jason continues:*

Everything in the notebook is a `_post`, apart from some of the descriptive pages I've put together (like this page). Everything here is a Markdown file contained in `_posts`.

At a conceptual level, I distinguish from "essays" and "notes." A note is any page in a notebook for recording something useful---reading notes, archive notes, primary sources notes, and so on, but a note cannot stand alone without extra context. So, context for notes live inside of a `project` that those notes relate to. Each of this metadata is contained in `category` in Jekyll's YAML, providing me a way to break down notes into units. Notes often appear in more than one category. For example, a note might look like:

~~~
---
layout: post
title: "white1995misfortune"
tags: [american west, dissertation, survey]
categories:
- Readings
---
~~~

Toward the bottom of the YAML header, the note belongs to the categorires `Readings`, relating the note to categories that I can then sort by and parse. These categories are used in the notebook itself to build lists from project pages.

Essays, in contrast, are related to specific projects or collections of notes, meant for me to make things more comprehensible or extend the context around historical information. For example, an essay might include the following metadata:

~~~
---
layout: essay
title: "Urbanization and the American West"
tags: [urban history, urbanization, suburbanization, american west, dissertation]
categories:
- Essays
---
~~~

The essay isn't related to a specific project necessarily. The category `Essays` will put it in a list of essays and general writings in the notebook. I also give the essay a different layout, which has a few minor UI tweaks from the post format.

Each post also has a series of [tags](/tagged/) which I often use for grouping together by topic or theme. [Categories](/categories/) are a higher level than tags, meant for grouping posts together more by their genre than their thematic or topical similarity. Categories are a controlled vocabulary and consist of a smaller set of words than tagging. Right now, the available categories are:

- Readings
- Essays
- Archive
- Administrative

## Documentation

There are a few scripts to make it easy to create new notes and essays. Most of these are contained in the `Rakefile`. The task `newnote` copies a template Markdown file with proper YAML header information and date stamp to the `_md` directory. The task `newessay` does the same thing. The task `prep` copies over the `_md` files into `_posts` with the appropriate date appended to the filename.

Additionally, since I'm using the R language more and more for visualization and statistical information, I've started using a script called `KnitPost` that reads files inside the `_Rmd` directory and converts them into Jekyll posts. This also preserves all of the R markup, figures, charts, and tables that come along with the document.

These scripts help keep categories, tags, and layout correct, and automate most of the maintenance I would otherwise be doing by hand.

_I'll just note here I've added to the rakefile to create a command that moves the generated `public` folder into the smgprojects.github.io repo on my machine, so I can push changes online. The code is:_

```
desc "Move public to github.io folder for syncing"
task :togithub do
    FileUtils.cp_r 'public/.', '/Users/shawngraham/Documents/smgprojects.github.io'
end
```

# Deployment

_If I were any good, I'd also have things set up to do the deploying as part of that task, rather like the gh-deploy code for [mkdocs](http://mkdocs.org)_.

Jason continues:

When I'm ready to push notes or edits to the live site, my `Rakefile` does the following:

- Files in `_md` and `_Rmd` are copied into `_posts` with the appropriate filenames.
- Changes to the local source are checked into git.
- The local sources are pushed to Github to maintain the record of each change.
- Jekyll builds a new version of the static website from the local source into a local `_site` directory, which contains the notebook.
- I use rsync on the `_site` directory to then deploy the notebook to the web, building the open access version of the notebook.

This takes around sixty seconds for the entire process to happen. It's a little slow at times, but by and large doesn't hamper my workflow.

_I don't use the rsync part of Jason's rakefile, but I do use the `rakefile draft` and `rakefile write` and rakefile `publish` (which moves the files out of the draft folder and into the posts folder.)_

## Details

The notebook uses Jekyll at its most recent release. I only modify Jekyll by adding plugins. In particular, it's important to make sure the Jekyll Scholar dependencies are updated along with any Jekyll system updates. I also use [Bootstrap]() to handle most of the CSS, icons, and layout of the notebook, with some heavy tweaks inside the `main.css` file. These are pre-processed `sass` files.

I take advantage of several plugins:

- **markdown**: I want to occasionally include Markdown files from the `_includes` directory, but using liquid's `include` expects `.html`. The plugin adds a new liquid controller called `markdown` that allows me to pass these files along and have them markdownified. I use this in particular for the front page.
- **Jekyll-Scholar**: I use this to take advantage of BibTeX files for referencing articles, books, and other materials.
- **git_modified**: A plugin borrowed from Carl Boettiger for looking at git modification time for a file, and using that to set a Liquid variable of last modification time. I use this in the metadata of posts and essays for indicating difference between when a file was originally written and last modified.

## Pandoc

I have replaced Jekyll's default Markdown parser with [Pandoc](http://johnmacfarlane.net/pandoc/), because Pandoc is awesome. It's a document utility written in Haskell for translating Markdown.

I have templates for writing in RMarkdown with embedded R code, using [Knitr]() to produce plain Markdown with source code annotations. These are useful as reproducable research within the notebook and easy to transition into print publications. I blame [Lincoln](http://lincolnmullen.com) for all this R stuff.
