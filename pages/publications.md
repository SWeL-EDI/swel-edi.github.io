---
title: Publications
description: Publications by members of the Semantic Web Lab
permalink: /publications/
layout: default
---

Lab members have published {% bibliography_count --file conferences.bib --file journals.bib %} papers in peer reviewed conferences and journals. Below you will find a complete listing of all our contributions ({% bibliography_count %}) to conferences, journals, workshops, proceedings, and technical recommendations, as well as PhD theses.

<!-- Get current year -->
{% assign currentYear = 'now' | date: "%Y" %}
<!-- For each year from now until 2002, print publications from that year -->
{% for focusYear in (2014..currentYear)  reversed %}
<!-- Only print years with publications -->
<!-- 
    Following code to capture the count came from 
    https://github.com/inukshuk/jekyll-scholar/issues/310#issuecomment-654578621 
-->
{%- capture pubCount -%}
{%- bibliography_count --query @*[year={{focusYear}}] -%}
{%- endcapture -%}

{% if pubCount != "0" %}
## {{ focusYear }}
{% bibliography --query @*[year={{focusYear}}] %}
{% endif %}

{% endfor %}
