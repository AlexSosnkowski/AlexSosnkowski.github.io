---
title: Projects
has_children: true
---
# My Projects

Below are some projects I have worked on during my time studying at UVA. Some where created as part of assignments while others were made simply for fun!

{% for post in site.posts %}

<ul>

<li><h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3></li>

</ul>

{% endfor %}
