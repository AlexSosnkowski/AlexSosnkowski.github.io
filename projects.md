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
        box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.15);
        background-color: #f9f9f9;
        border-radius: 1vh;
        width: 100%;
        height: 100%;
    }

    .project p{
        font-size: small;
    }

    .thumbnail {
        flex: 1;
        width: 100%;
        height: 100%;
        justify-content: center;
        align-items: center;
    }
    
    .thumbnail img {
        width: 100%;
        height: 100%;
        object-fit: cover;
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
        border-radius: 2%;
    }

    .blurb {
        width: 100%;
        height: 100%;
        padding-left: 5%;
        padding-bottom; 5%;
        flex: 2;
        justify-content: center;
        align-items: center;
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
                <h4><a href="{{ project.url | relative_url }}">{{ project.title }}</a></h4>
                <p>{{ project.blurb }}</p>
            </div>
        </div>
    {% endfor %}

</div>