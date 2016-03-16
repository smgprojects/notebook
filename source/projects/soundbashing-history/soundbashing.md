---
layout: page
title: Soundbashing History
permalink: /soundbashing-history/
---

* Table of Contents
{:toc}

>  This page is just an empty template

Text here describing the project. See Heppler's machinesvalley.md for original

## Research Archives

Notes organized by [research archive](/research-archives/).

## Related Notes

<table class="table-stripped">
    <tr>
      <th>Date</th>
      <th>Title</th>
    </tr>
    {% for post in site.tags["soundbashing"] %}
    <tr>
      <td width="15%;">{{ post.date | date_to_string }}</td>
      <td width="70%;"><a href="{{ post.url | prepend: site.baseurl }}">{{post.title}}</a></td>
      </tr>
    {% endfor %}
  </table>
