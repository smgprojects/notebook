---
layout: page
title: Visualization in the Humanities
permalink: /visualization-humanities/
tags: [visualization]
---

* Table of Contents
{:toc}

## Project Description

In what ways can historians take advantage of visualization techniques in the presentation and communication of historical arguments? Can we, through data-drive and visualization-driven research, shape new methods of revealing ambiguity, complexity, and exploration of the past?

My notes and research into visualization in the humanities feeds several areas of current work:

- A book chapter on evidence visualization in history (in progress)
- A potential course on data visualization in history (planning)
- A journal article on visualizing evidence in history (in progress)
- My larger professional interest in digital history and new methods of knowledge production

## Related Notes

<table class="table-stripped">
    <tr>
      <th>Date</th>
      <th>Title</th>
    </tr>
    {% for post in site.tags.visualization %}
    <tr>
      <td width="15%;">{{ post.date | date_to_string }}</td>
      <td width="70%;"><a href="{{ post.url | prepend: site.baseurl }}">{{post.title}}</a></td>
      </tr>
    {% endfor %}
  </table>