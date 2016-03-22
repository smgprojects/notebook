---
layout: page
title: Soundbashing History
permalink: /soundbashing-history/
---

* Table of Contents
{:toc}


If instead of _visualizing_ the past, we tried to listen to it? Not in an archaeo-acoustic sense, but rather, let's forget the screen for a moment, and instead try to develop a grammar, a framework, some compositional rules, to enable us to hear the meaningful patterns in our data? This necessarily moves us along a spectrum from 'mere' dataviz to actual performance, which moves us into interesting public history territory.

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
