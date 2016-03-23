---
layout: page
title: Design Studio in Digital History
permalink: /designstudio/
---

* Table of Contents
{:toc}


I'm inspired by the work of [Bill Turkel, Rob MacDougall, Devon Elliott](http://www.cjc-online.ca/index.php/journal/article/view/2506); [Jentry Sayers et al](http://www.maker.uvic.ca/hastac/#/splash); [Kim Martin, Beth Compton, and Ryan Hunt](http://dhmakerbus.com/); and [Megan Smith](http://megansmith.ca/) in terms of making and physical computation and fabrication. Coming from archaeology, which has a strong tradition of experimentation (in the sense that makers would recognize) the penny finally dropped: why am I not doing this in my teaching? I have a series of courses, from first year to graduate level, that explore different aspects of the digital and making in the sense of coding, using web techs, etc, but I have nothing that returns me to my roots in archaeology. This project then involves me putting together the critical context, and designing, for a year long fourth year seminar that I'm provisionally calling 'Design Studio in Digital History'. This would involve using the makerspaces at Carleton (Discovery Centre) and the city of Ottawa, to provide a materially-grounded exploration of the past through making.

What would such a course look like? What would it do? How do I design it? Do I design it while I run it, in tandem with the students? I have no appropriate makerspace or workbench: is it possible to run such a course by locating and occupying spaces around the city? What - and how - does that intersect with the pedagogy? What basic materials do I need? How much will this cost? What kinds of things might students make? The city of Ottawa has lumbering and manufacturing in its genealogy: what if I focussed on merging wood & the digital? .... stay tuned - or leave comments via the Hypothesis webannotation framework on the right.

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
