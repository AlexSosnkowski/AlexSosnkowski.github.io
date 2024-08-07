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
        padding: 4%;
        width: 30vw;
        height: 30vh;
    }

    .thumbnail {
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
        flex: 1;
        width: 50%;
        height: 50%;
    }
    
    .thumbnail img {
        object-fit: cover;
        display: block;
        margin-left: auto;
        margin-right: auto;
    }

    .blurb {
        padding-left: 2%;
        width: 50%;
        height: 50%;
        flex: 2;
    }

    .divider {
        width: 100%;
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
        opacity: 0%;

    }

</style>

Below are some projects I have worked on during my time studying at UVA. Some where created as part of assignments while others were made simply for fun!

<div class="project-container">
    {% for project in site.projects %}

        <div class="project">
            <div class="thumbnail">
                <img src="/projects/{{ project.thumbnail }}" alt="{{ project.title }}">
            </div>
            <div class="blurb">
                <h3><a href="{{ project.url | relative_url }}">{{ project.title }}</a></h3>
                <p>{{ project.excerpt }}</p>
            </div>
        
        </div>
        <hr class="divider" />
    {% endfor %}

</div>