---
layout: default
title: Projects
permalink: /projects/
---

## Current funded projects

{% for project in site.projects %}
{% unless project.expired %}
* [{{ project.title }}]({{ project.url }}) - {{ project.description }}
{% endunless %}
{% endfor %} 
