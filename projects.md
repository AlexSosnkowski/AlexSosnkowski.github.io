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
        display: flex;
        padding: 2%;
    }

    .thumbnail {
        box-shadow: 2vh 2vw;
        flex: 1;
    }
    
    .thumbnail img {
        object-fit: cover;
        width: 20vh;
        height: 20vw;
    }

    .blurb {
        flex: 2;
    }

</style>
# My Projects

Below are some projects I have worked on during my time studying at UVA. Some where created as part of assignments while others were made simply for fun!

<div class="project-container">
    {% for project in site.projects %}

        <div class="project">
            <div class="thumbnail">
                <img src="{{ project.thumbnail }}" alt="{{ project.title }}">
            </div>
            <div class="blurb">
                <h3><a href="{{ project.url | relative_url }}">{{ project.title }}</a></h3>
                <p>{{ project.excerpt }}</p>
            </div>
        </div>

    {% endfor %}

</div>