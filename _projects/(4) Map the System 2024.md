---
name: Map the System 2024
tags: [systems-thinking, design-thinking]
image: https://i.pinimg.com/736x/7d/80/78/7d8078c3c0040b4520f7d40102a261d6.jpg
description: Resources for my GEOG-639 class...
---

# Map the System 2024

Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

<h2>Related Blog Posts</h2>

{% for post in site.tags.map-the-system %}
<ul>
    <li>
        <a href='{{ site.baseurl }}{{ post.url }}'>{{ post.title }}</a>
    </li>
</ul>
{% endfor %}
