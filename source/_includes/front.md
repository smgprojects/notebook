## Welcome

My name is [Shawn Graham](http://electricarchaeology.ca) and I am an associate professor of Digital Humanities in the Department of History at [Carleton University](http://carleton.ca/history). This is my open research notebook for my sabbatical in the 2016-17 academic year. [My GitHub repositories are here.](http://github.com/shawngraham)

Readers may leave annotations on any part of this notebook using the [hypothesis](https://hypothes.is/) web annotation architecture. See that strip down the right hand side of the page? Click on there to get started!

### Active Projects

- [Soundbashing the Past](/soundbashing-history/)
- [Archaeogaming](/archaeogaming/)

<dl>
  {% assign projects_sorted = site.project | sort: 'status' %}
  {% for project in projects_sorted %}
    <dt>
      <a class="project-link" href="{{ project.url | prepend: site.baseurl | prepend: site.url }}">
        {{ project.title }}
      </a>
      {% if project.status == "active" %}
        <span class="label label-success">{{ project.status }}</span>
      {% elsif project.status == "collecting" %}
        <span class="label label-info">{{ project.status }}</span>
      {% elsif project.status == "on hold" %}
        <span class="label label-warning">{{ project.status }}</span>
      {% endif%}
    </dt>
    <dd>{{ project.description }}</dd>
  {% endfor %}
</dl>
