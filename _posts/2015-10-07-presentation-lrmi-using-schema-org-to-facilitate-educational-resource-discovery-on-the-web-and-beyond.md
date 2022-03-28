---
id: 143
title: 'Presentation: LRMI – using schema.org to facilitate educational resource discovery on the web and beyond'
date: '2015-10-07T09:32:28+01:00'
author: 'Phil Barker'
excerpt: 'Today I am in London for the ISKO Knowledge Organisation in Learning and Teaching meeting, where I am presenting on LRMI and schema.org to facilitate educational resource discovery on the web and beyond. My slides are here, mostly they cover similar ground to presentations I&rsquo;ve given before which have been captured on video or which &hellip; <a href="http://blogs.pjjk.net/phil/presentation-lrmi-using-schema-org-to-facilitate-educational-resource-discovery-on-the-web-and-beyond/">Continue reading <span>Presentation: LRMI &ndash; using schema.org to facilitate educational resource discovery on the web and beyond</span> <span>&rarr;</span></a>'
layout: post
guid: 'http://blogs.pjjk.net/phil/?p=1542'
permalink: 'http://blogs.pjjk.net/phil/presentation-lrmi-using-schema-org-to-facilitate-educational-resource-discovery-on-the-web-and-beyond/'
enclosure:
    - "\n\n"
syndication_source:
    - 'Sharing and learning'
syndication_source_uri:
    - 'http://blogs.pjjk.net/phil'
syndication_source_id:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed_id:
    - '2'
syndication_permalink:
    - 'http://blogs.pjjk.net/phil/presentation-lrmi-using-schema-org-to-facilitate-educational-resource-discovery-on-the-web-and-beyond/'
syndication_item_hash:
    - cc50d40685e32936c47020c0ae7f476a
    - 1d4e8646f0ebb37ebca52206cb675f99
    - 1d4e8646f0ebb37ebca52206cb675f99
    - 3618eeed79002469bab033125223086f
    - 3618eeed79002469bab033125223086f
    - f755d4e0135f550c704e7c156d595824
categories:
    - cetis
    - LRMI
    - 'resource description'
    - schema.org
---

Today I am in London for the [ISKO Knowledge Organisation in Learning and Teaching](http://www.iskouk.org/content/knowledge-organization-learning-and-teaching) meeting, where I am presenting on LRMI and schema.org to facilitate educational resource discovery on the web and beyond. My [slides are here](https://drive.google.com/open?id=1fmeb4IMYOlFOvK3YReHIl6AehNF-6RrSO1qfsjKHLWI), mostly they cover similar ground to presentations I’ve given before which have been [captured on video](http://videolectures.net/ocwc2014_barker_schema/) or which I have [written up in more detail](http://blogs.pjjk.net/phil/lrmi-learning-resource-metadata-on-the-web-from-the-lile2015-workshop/). So here I’ll just point to [my slides for today](https://docs.google.com/presentation/d/1fmeb4IMYOlFOvK3YReHIl6AehNF-6RrSO1qfsjKHLWI/edit?usp=sharing) (&amp; below) and summarise the new stuff.

<iframe allowfullscreen="true" frameborder="0" height="480" mozallowfullscreen="true" src="https://docs.google.com/presentation/d/1fmeb4IMYOlFOvK3YReHIl6AehNF-6RrSO1qfsjKHLWI/embed?start=false&loop=false&%23038;delayms=3000" webkitallowfullscreen="true" width="640"></iframe>

## LRMI uptake

People always want to know how much LRMI exists in the wild, and now schema.org reports this infomation. Go to the schema.org page for any class or property and at the top it says in how many domains they find markup for it. Obviously this misses that not all domains are equal in extent or importance: finding LRMI on pjjk,net should not count as equal to finding it on bbc.co.uk, but as a broad indicator it’s OK: finding a property on 10 domains or 10,000 domains is a valid comarison. LRMI properties are mostly reported as found on 100-1000 domains (e.g. [learning resource type](http://schema.org/learningResourceType)) or 10-100 domains (e.g. [educational alignment](http://schema.org/educationalAlignment)). A couple of LRMI properties have greater usage, e.g. [typical age range](http://schema.org/typicalAgeRange) and [is based on URL](http://schema.org/isBasedOnUrl) (10-50,00 and 1-10,000 domains respectively), but I guess that reflects their generic usefulness beyond learning resources. We know that in some cases LRMI is [used for internal systems but not exposed on web pages](http://publications.cetis.org.uk/2014/1007), but still the level of usage is not as high as we would like.

I also often get asked about support for creating LRMI metadata, this time I’m including a mention of how it is possible to write [WordPress plugins and themes with schema / LRMI support](http://blogs.pjjk.net/phil/wordpress-as-a-semantic-web-platform/), and the [drupal schema.org plugin](https://www.drupal.org/project/schemaorg). I’m also aware of “tagging tools” associated with various repositories, e.g. the [learning registry](http://learningregistry.org/) and the [Illinois Shared Learning Environment](https://ioer.ilsharedlearning.org/). I think it’s always going to be difficult to answer this one as the best support will always come from customising whatever CMS an organisation uses to manage their content or metadata and will be tailored to their workflow and the types of resources and educational contexts they work in.

As far implementation for search I still cover google custom search, as in the previous presentations.

## Current LRMI activities

The [DCMI LRMI task group](http://wiki.dublincore.org/index.php/AB-Comm/ed/LRMI/TG) is active, one of our priorities is to improve the support for people who want to use LRMI. Two activities are nearing fruitition: firstly, we are hoping to provide [examples for relevant properties and type](http://blogs.pjjk.net/phil/lrmi-examples-for-schema-org/) on the schema.org web site. Secondly, we want to provide better support for the vocabularies used for properties such as alignment type (in the Alignment Object), learning resource type etc, by way of clear definitions and machine readable vocabulary encodings (using SKOS). We are asking for [public review and comment on LRMI vocabularies](https://groups.google.com/forum/#!topic/lrmi/JgmUWSm0JJY), so please take a look and get in touch.

Other work in progress is around [schema for courses](https://docs.google.com/document/d/1U-s5HjNkWUtIoLAHjRcUZljBWEdHQIupk-KscAEIbFA/edit?usp=sharing) and extending some of the vocabularies mentioned above. We have monthly calls, if you would like to lend a hand please do get in touch.