---
title: Calls
permalink: /calls/
redirect_from: "/Calls"
---

{% include JB/tag_list tag="call" %}

<ul>
{% for page in tag_pages %}
    <li><a href="{{ page.url }}">{{page.title}}</a></li>
{% endfor %}
</ul>
