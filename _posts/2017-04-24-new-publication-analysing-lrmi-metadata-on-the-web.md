---
id: 586
title: 'New publication analysing LRMI metadata on the web'
date: '2017-04-24T14:57:54+01:00'
author: 'Phil Barker'
excerpt: "<p>I have a new publication: &ldquo;Analysing and Improving Embedded Markup of Learning Resources on the Web,&rdquo; which Stefan Dietze and Davide Taibi have presented at the 2017 International World Wide Web Conference in Perth Australia. I played a minor role in the &ldquo;analysing&rdquo; part of this work, the heavy lifting was done by my co-authors. &hellip; <a href=\"https://blogs.pjjk.net/phil/analysing-improving-embedded-markup-learning-resources-web/\">Continue reading <span>New publication analysing LRMI metadata on the web</span> <span>&rarr;</span></a></p>\n<p>The post <a rel=\"nofollow\" href=\"https://blogs.pjjk.net/phil/analysing-improving-embedded-markup-learning-resources-web/\">New publication analysing LRMI metadata on the web</a> appeared first on <a rel=\"nofollow\" href=\"https://blogs.pjjk.net/phil\">Sharing and learning</a>.</p>"
layout: post
guid: 'https://blogs.pjjk.net/phil/?p=1773'
permalink: 'https://blogs.pjjk.net/phil/analysing-improving-embedded-markup-learning-resources-web/'
enclosure:
    - "\n\n"
syndication_source:
    - 'Sharing and learning'
syndication_source_uri:
    - 'https://blogs.pjjk.net/phil'
syndication_source_id:
    - 'http://blogs.pjjk.net/phil/feed/'
'rss:comments':
    - 'https://blogs.pjjk.net/phil/analysing-improving-embedded-markup-learning-resources-web/#respond'
'wfw:commentRSS':
    - 'https://blogs.pjjk.net/phil/analysing-improving-embedded-markup-learning-resources-web/feed/'
syndication_feed:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed_id:
    - '2'
syndication_permalink:
    - 'https://blogs.pjjk.net/phil/analysing-improving-embedded-markup-learning-resources-web/'
syndication_item_hash:
    - 08aa84c08bfb74c48f33744b971b2276
categories:
    - LRMI
    - metadata
    - schema.org
    - 'semantic technologies'
---

I have a new publication: “Analysing and Improving Embedded Markup of Learning Resources on the Web,” which Stefan Dietze and Davide Taibi have presented at the 2017 International World Wide Web Conference in Perth Australia. I played a minor role in the “analysing” part of this work, the heavy lifting was done by my co-authors. They analysed data from the [Common Crawl](http://commoncrawl.org/) to identify sites that were using [LRMI terms](http://dublincore.org/dcx/lrmi-terms/1.1/) in their schema.org markup. The analysis provides answers to important questions such as: who is using LRMI metadata and which terms are they using? How many resources have been marked up with LRMI metadata? Are the numbers of users growing? What mistakes are being made in implementing LRMI?

We also see how once a term is in schema.org it is interpreted in ways that may not have been anticipated by those who created it, with any implicit assumptions held within a community of practice being ignored. Thus terms that have a specific meaning within the learning, education and training field are construed in their more generic meaning. The result of this is that some LRMI terms are used for resources that we in LRMI did not have in mind when creating them. Consequently the presence of LRMI metadata on a web resource may not be a good indicator that a resource is intended for education–this is true of some properties more than others. To avoid this when making additions to schema.org (*if* you see it as a problem), the domain to which a term applies should be in the term name.

A second observation that seems important to me is the strong inverse relationship between sophisticated data structures and amount of usage. Yes, I’m talking about the [AlignmentObject](https://blogs.pjjk.net/phil/explaining-the-lrmi-alignment-object/): potentially very expressive, but either it solves a problem no one has (which I don’t think is the case) or it is so complex that few people understand it well enough to use it. In general, properties with simple text/literal values get much more use than entity-valued properties.

## Publication Details

The official reference is: Stefan Dietze, Davide Taibi, Ran Yu, Phil Barker, and Mathieu d’Aquin. 2017.[ Analysing and Improving Embedded Markup of Learning Resources on the Web](http://dl.acm.org/citation.cfm?id=3054160). In Proceedings of the 26th International Conference on World Wide Web Companion (WWW ’17 Companion). International World Wide Web Conferences Steering Committee, Republic and Canton of Geneva, Switzerland, 283-292. DOI: 10.1145/3041021.3054160

It is licensed CC:BY, but the ACM version seems to be behind a paywall, so **here is a [local post-publication copy](https://blogs.pjjk.net/phil/content/uploads/p283-dietze.pdf) (pdf)**.

Here’s the abstract.

> Web-scale reuse and interoperability of learning resources have been major concerns for the technology-enhanced learning community. While work in this area traditionally focused on learning resource metadata, provided through learning resource repositories, the recent emergence of structured entity markup on the Web through standards such as RDFa and Microdata and initiatives such as schema.org, has provided new forms of entity-centric knowledge, which is so far under-investigated and hardly exploited. The Learning Resource Metadata Initiative (LRMI) provides a vocabulary for annotating learning resources through schema.org terms. Although recent studies have shown markup adoption by approximately 30% of all Web pages, understanding of the scope, distribution and quality of learning resources markup is limited. We provide the first public corpus of LRMI extracted from a representative Web crawl together with an analysis of LRMI adoption on the Web, with the goal to inform data consumers as well as future vocabulary refinements through a thorough understanding of the use as well as misuse of LRMI vocabulary terms. While errors and schema misuse are frequent, we also discuss a set of simple heuristics which significantly improve the accuracy of markup, a prerequisite for reusing learning resource metadata sourced from markup.

The post [New publication analysing LRMI metadata on the web](https://blogs.pjjk.net/phil/analysing-improving-embedded-markup-learning-resources-web/) appeared first on [Sharing and learning](https://blogs.pjjk.net/phil).