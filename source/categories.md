---
layout: page
title: Categories
permalink: /categories/
---

<p>Notes organized by category.</p>

{% for category in site.categories %}

### {{ category | first }}

<ul>
{% for posts in category %}
  {% for post in posts %}
    {% if post.title %}
    <li><a href="{{ site.baseurl}}{{ post.url }}">{{ post.title }}</a></li>
    {% endif %}
  {% endfor %}
{% endfor %}
</ul>

{% endfor %}