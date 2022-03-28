---
id: 1302
title: 'Subsetting KGs: Talk at Wikidata Reuse Days'
date: '2022-03-13T18:44:25+00:00'
author: 'Seyed Hosseini Beghaeiraveri'
layout: post
guid: 'http://www.macs.hw.ac.uk/SWeL/?p=1302'
permalink: /2022/03/13/subsetting-kgs-talk-at-wikidata-reuse-days/
categories:
    - big-data
    - knowledge-graph
tags:
    - Biohackathon
    - Subsetting
    - Wikidata
    - 'Wikidata Reuse Days'
---

The [BioHackathon Europe](https://2021.biohackathon-europe.org/) [Subsetting Project](https://github.com/elixir-europe/bioHackathon-projects-2021/tree/main/projects/21) intends to present the achievements and challenges of Wikidata subsetting on the [Wikidata Reuse Days](https://diff.wikimedia.org/event/wikidata-data-reuse-days-2022/). I’m going to be in this presentation too, and I’m going to talk about the role of Wikidata References in subsetting and also about one of the Wikidata third-party tools, called [WDumper](https://wdumps.toolforge.org/) as a subsetting tool. Join us if you want to know more about subsetting applications, theoretics, tools, and challenges.

[This link](https://diff.wikimedia.org/event/%e2%99%bb%ef%b8%8f-biohackathon-report-on-reviewing-wikidata-subsetting-methods/) refers to the details of the event, the speakers, and the topics covered. If you want to know more about the Subsettint Project in BioHackathon Europe, See [this post](https://seyedahbr.github.io/Blog/Biohackathon21.html).

**Abstract**

Often Wikidata is too big to handle. Through a sequence of BioHackathons, we have been reviewing methods to extract subsets from Wikidata to facilitate downstream reuse. We have identified a set of tools and would like to report back on our intermediate results. We will address the different applicable file formats. Natively, Wikidata data is stored in JSON, but it is also available as RDF through for example the Wikidata Query Service. Different subsetting methods use either or both of those formats as input and output. We will also address the way how to define the subset. This can be a JSON file or a Shape Expression.