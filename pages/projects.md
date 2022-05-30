---
layout: default
title: Projects
permalink: /projects/
---

{%- assign currentDate = site.time | date: '%F' %}

## Current Projects

{% for project in site.projects %}
    {%- assign endDate = project.end_date | date: '%F' %}
    {% unless endDate < currentDate %}
* [{{ project.title }}]({{ project.url }}) - {{ project.description }}
    {% endunless %}
{% endfor %} 

## Past Projects

{% for project in site.projects %}
    {%- assign endDate = project.end_date | date: '%F' %}
    {% unless endDate >= currentDate %}
* [{{ project.title }}]({{ project.url }}) - {{ project.description }}
    {% endunless %}
{% endfor %} 
