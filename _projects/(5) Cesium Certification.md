---
name: Cesium Developer Certification Progress
tags: [gis, cesiumjs, o3de, 3D, cloud-native]
image: http://www.geosolutionsgroup.com/wp-content/uploads/2023/06/cesium-certified-dev-logo-sm.png?x31768
description: Resources for my GEOG-639 class...
---

# Cesium Developer Certification Progress

I'm in the process of finishing certification for becoming a cesium developer. As this is now an OGC standard, it will a useful GIS technology to know. Here are the basic pieces of it...

<!-- BLOG POSTS -->
{% for post in site.tags.cesiumjs %}
<ul>
    <li>
        <a href='{{ site.baseurl }}{{ post.url }}'>{{ post.title }}</a>
    </li>
</ul>
{% endfor %}