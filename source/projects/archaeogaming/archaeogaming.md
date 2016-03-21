---
layout: page
title: Archaeogaming
permalink: /archaeogaming/
---

* Table of Contents
{:toc}

>  This page is just an empty template

Text here describing the project. See Heppler's machinesvalley.md for original

## Research Archives

Notes organized by [research archive](/research-archives/).

[No Man's Sky Stuff](#todo:10)

## Related Notes

<table class="table-stripped">
    <tr>
      <th>Date</th>
      <th>Title</th>
    </tr>
    {% for post in site.tags["archaeogaming"] %}
    <tr>
      <td width="15%;">{{ post.date | date_to_string }}</td>
      <td width="70%;"><a href="{{ post.url | prepend: site.baseurl }}">{{post.title}}</a></td>
      </tr>
    {% endfor %}
  </table>
