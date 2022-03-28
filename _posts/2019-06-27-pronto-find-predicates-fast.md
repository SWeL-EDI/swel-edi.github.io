---
id: 1013
title: 'Pronto &#8211; Find Predicates Fast'
date: '2019-06-27T12:23:56+01:00'
author: 'Francesco Belvedere'
excerpt: 'If you work with linked data or the semantic web, you understand how dull digging through ontologies to find concepts and predicates can be. At Wallscope we understand this too – so we created Pronto, a free tool that makes this work easier and more ef...'
layout: post
guid: 'https://medium.com/p/15187f52f516'
permalink: 'https://medium.com/wallscope/pronto-find-predicates-fast-15187f52f516?source=rss----d173846af2b9--rdf'
syndication_source:
    - 'Rdf in Wallscope on Medium'
syndication_source_uri:
    - 'https://medium.com/wallscope/tagged/rdf?source=rss----d173846af2b9--rdf'
syndication_source_id:
    - 'https://medium.com/feed/wallscope/tagged/rdf'
syndication_feed:
    - 'https://medium.com/feed/wallscope/tagged/rdf'
syndication_feed_id:
    - '4'
syndication_permalink:
    - 'https://medium.com/wallscope/pronto-find-predicates-fast-15187f52f516?source=rss----d173846af2b9--rdf'
syndication_item_hash:
    - 082e7f6037253e350833379a3b207faa
    - 1ce74fe67fd92bad620620d1f38befca
    - 082110df270e14355e844260fbc5b091
    - 22f6662bd70f1bc76b02fdba84e07218
    - 833ed14d420ddc5ca4cc100073b653f5
categories:
    - data-science
    - ontology
    - rdf
    - search-engines
    - semanticweb
    - Wallscope
---

<figure>![](https://cdn-images-1.medium.com/max/1024/1*LZscdHk1Vn86pOKCILIAIw.jpeg)</figure>If you work with linked data or the semantic web, you understand how dull digging through ontologies to find concepts and predicates can be. At [Wallscope](https://www.wallscope.co.uk/) we understand this too – so we created [Pronto](https://pronto.wallscope.co.uk/), a free tool that makes this work easier and more efficient. (If you are new to the semantic web and link data, I suggest you have a look at the type of [challenges it aims to solve first](https://medium.com/wallscope/tackling-big-data-challenges-with-linked-data-278b0761a6de).) **The Problem**. The objective of an ontology is to be reused. Although this is a simple concept, it can prove inconvenient in the long run. The many existing ontologies make searching for concepts and predicates tedious, labour-intensive and time-consuming. One has to iteratively and manually inspect a number of ontologies until a suitable ontological component is found. At Wallscope this issue impacts us since our work includes building data exploration systems that connect independent and diverse data sources. So we started thinking. > It would be much easier to search through all ontologies — or at least the main ones — at the same time.

As a result, we decided to invest in the creation of Pronto with the aim to overcome this challenge. <figure>![](https://cdn-images-1.medium.com/max/822/1*ET9hKTDjhDlYQG9M53Hk-g.png)<figcaption>Example search of a predicate with Pronto.</figcaption></figure>**The Solution**. Pronto allows developers to search for concepts and predicates among a number of ontologies, originally selected from the [prefix.cc](http://prefix.cc/) user-curated “popular” list, along with some others we use. These include: - rdf and rdfs
- foaf
- schema
- geo
- dbo and dbp
- owl
- skos
- xsd
- vcard
- dcat
- dc and dcterms
- madsrdf
- bflc

Searching for a concept or a predicate retrieves results from the above ontologies, ordered by relevance. [**Try it here**](https://pronto.wallscope.co.uk/) **to see how Pronto works in practice.**Thanks for reading. We would be interested to hear your feedback or suggestions for others ontologies to include. If you find Pronto useful give the article some claps (up to 50 if you hold the button 😄) so that more people can benefit from this tool! ![](https://medium.com/_/stat?event=post.clientViewed&referrerSource=full_rss&postId=15187f52f516)- - - - - -

[Pronto - Find Predicates Fast](https://medium.com/wallscope/pronto-find-predicates-fast-15187f52f516) was originally published in [Wallscope](https://medium.com/wallscope) on Medium, where people are continuing the conversation by highlighting and responding to this story.