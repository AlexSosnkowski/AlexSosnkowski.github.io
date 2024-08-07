---
title: Projects
---
<style>
    .project-container {
        display: flex;
        flex-wrap: wrap;
        gap: 2vh;
    }

    .project {
        padding: 2%;
    }

    .project img {
        border-radius: 3%;
        border-style: solid;
        border-color: darkblue;
    }

</style>
# My Projects

Below are some projects I have worked on during my time studying at UVA. Some where created as part of assignments while others were made simply for fun!

<div class="project-container">
{% for project in site.projects %}

<div class="project">

<img src="{{ project.thumbnail }}" alt="{{ project.title }}">

<h3><a href="{{ project.url | relative_url }}">{{ project.title }}</a></h3>

</div>

{% endfor %}

</div>