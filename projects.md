---
title: Projects
---
# My Projects

Below are some projects I have worked on during my time studying at UVA. Some where created as part of assignments while others were made simply for fun!

{% for project in site.projects %}

<ul>

<li><h3><a href="{{ project.url | relative_url }}">{{ project.title }}</a></h3></li>

</ul>

{% endfor %}
