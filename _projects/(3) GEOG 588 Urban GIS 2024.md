---
name: Urban GIS + Experiential Learning (Winter 2024)
tags: [Urban, GIS, Experiential-Learning, Teaching]
style: fill
color: info
description: Resources for my GEOG-639 class...
---

# GEOG-588 > Urban GIS

I am TA'ing for [GEOG-588 Urban GIS](https://geog.ucalgary.ca/manageprofile/courses/w24/GEOG588), and she has *completely* redesigned the course to focus on experiential learning which presents guest-experts from industry to come and pose design-challenge questions to our students. 

#### Why it is exciting

It is proving to be an exciting course because of the ground breaking, experiential approach being used: she is inviting some great local experts to come talk to the class as and pose urban design questions to the students, to challenge them to think creatively and create solutions that they've developed.

#### My Role

As TA, my role is 1) support GEOG-588's new approach, and 2) help catalyze student innovation by conducting labs where students will develop their self-directed projects help students more deeply understand the course materials (and trouble shoot any technical issues they might have with GIS, Programming, or acquiring useful data.)

I'll be posting occasional insights in small blog posts that you find in the blog section of my site.

Here is the university's [official course-description](https://geog.ucalgary.ca/manageprofile/courses/w24/GEOG588):


<h2>Related Blog Posts</h2>

{% for post in site.tags.GEOG-588-Urban-GIS %}
<ul>
    <li>
        <a href='{{ site.baseurl }}{{ post.url }}'>{{ post.title }}</a>
    </li>
</ul>
{% endfor %}
