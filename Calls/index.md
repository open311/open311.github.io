---
title: Calls
permalink: /calls/
redirect_from: "/Calls"
---

Calls
=============

<ul>
{% for page in site.pages %}
    {% for tag in page.tags %}
        {% if tag == "call" %}
            <li><a href="{{ page.url }}">{{page.title}}</a></li>
        {% endif %}
    {% endfor %}
{% endfor %}
</ul>
