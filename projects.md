---
title: Projects
---
<style>
    .post {
        width: 10vh;
        padding: 2%;
        border-radius: 3%;
        border-style: solid;
        border-color: orange;
    }
</style>
# My Projects

Below are some projects I have worked on during my time studying at UVA. Some where created as part of assignments while others were made simply for fun!

{% for project in site.projects %}

<div class="post">

<img src="{{ project.thumbnail }}" alt="{{ project.title }}">

<h3><a href="{{ project.url | relative_url }}">{{ project.title }}</a></h3>

</div>

{% endfor %}
