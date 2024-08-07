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
    }

    .project p{
        font-size: small;
    }

    .thumbnail {
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
        flex: 1;

    }
    
    .thumbnail img {
        object-fit: cover;
        border-radius: 2%;
    }

    .blurb {
        padding-left: 5%;

        flex: 2;
    }

    .divider {
        height: 0px;
        width: 100%;
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 5px 0 rgba(0, 0, 0, 0.19);
        border-style: inset;
        border-radius: 2%;
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
        <hr class="divider" />
    {% endfor %}

</div>