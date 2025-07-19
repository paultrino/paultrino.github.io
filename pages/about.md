---
layout: page
title: About
permalink: /about/
weight: 1
---

# **About Me**

Hi I am **{{ site.author.name }}** :wave:, a PhD candidate in the Geography Department.<br>

Well travelled, personable, good at listening, and quick to learn new things: I am a software engineer, GIS analyst, (and [amateur sculptor](https://sites.google.com/view/functionalfox/about)!), with 15 years of software-dev experience, and 2 master’s degrees, starting a PhD at the University of Calgary under the direction of <a target="_blank" href="https://profiles.ucalgary.ca/rupert-daniel-jacobson">Dr. Dan Jacobson </a>.  I also work part-time as a senior software engineer, and also volunteer as the VP of Student Life, the Equality, Diversity, and Inclusion (EDI) committee as the graduate representative.

My research focus is on accessibility and **disability barriers** in the built environment. I’m leveraging conceptual frameworks in social justice, technologies such as GIS, Cloud Computing, Machine Learning, and LiDAR to complete automated citywide accessibility evaluations that are free from disability and inclusion biases.

It is a subject close to me: When I was younger, I almost lost my legs, and I prepared myself for this seeming eventuality for almost a decade. The experience left me with and open mind, and a deep appreciation for the everyday courage of people who choose to go on, no matter their challenges or lack of equity.


<!-- <div class="row">
{% include about/skills.html title="Programming Skills" source=site.data.programming-skills %}
{% include about/skills.html title="Other Skills" source=site.data.other-skills %}
</div>

<div class="row">
{% include about/timeline.html %}
</div> -->

## Subjects I write about...

My projects and blog posts have the following tags (aka. subjects)...

<div class="tags">
{% for tag in site.tags %}
  {% assign t = tag | first %}
  {% assign posts = tag | last %}
  <a    class="badge badge-secondary" 
        href="{{site.baseurl}}/blog/tags#{{t}}" 
        target="_blank">{{t | upcase | replace:" ","-" }} ({{ posts | size }})</a>
{% endfor %}
</div>