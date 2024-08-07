---
title: Projects
---
<style>
    .post {

    }
</style>
# My Projects

Below are some projects I have worked on during my time studying at UVA. Some where created as part of assignments while others were made simply for fun!

{% for project in site.projects %}

<div class="post">

<img src="{{ post.thumbnail }}" alt="{{ post.title }}">

<h3><a href="{{ project.url | relative_url }}">{{ project.title }}</a></h3>

</div>

{% endfor %}
