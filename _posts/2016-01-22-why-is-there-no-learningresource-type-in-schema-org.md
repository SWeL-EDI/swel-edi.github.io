---
id: 133
title: 'Why is there no LearningResource type in schema.org?'
date: '2016-01-22T10:45:30+00:00'
author: 'Phil Barker'
excerpt: 'A couple of times in the last month or so the question of why isn&rsquo;t there a LearningResource type in schema.org as a subtype of CreativeWork. In case it comes up again, here&rsquo;s my answer. We took a deliberate decision way back at the start of LRMI not to define a LearningResource as a subtype &hellip; <a href="http://blogs.pjjk.net/phil/why-is-there-no-learningresource-type-in-schema-org/">Continue reading <span>Why is there no LearningResource type in schema.org?</span> <span>&rarr;</span></a>'
layout: post
guid: 'http://blogs.pjjk.net/phil/?p=1599'
permalink: 'http://blogs.pjjk.net/phil/why-is-there-no-learningresource-type-in-schema-org/'
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
    - 'http://blogs.pjjk.net/phil/why-is-there-no-learningresource-type-in-schema-org/'
syndication_item_hash:
    - 07e3d5fa300f0746f5369b825a0a96fd
    - a585312bfea0f3f2fd0f3f6afd6fce7a
    - a585312bfea0f3f2fd0f3f6afd6fce7a
    - 37a86c4efc1d605eae2ab27af64b14cc
    - 37a86c4efc1d605eae2ab27af64b14cc
    - b70fd96ca0ae5f9c7ea18b08124b4e45
categories:
    - Other
---

A couple of times in the last month or so the question of why isn’t there a LearningResource type in schema.org as a subtype of [CreativeWork](http://schema.org/CreativeWork). In case it comes up again, here’s my answer.

We took a deliberate decision way back at the start of LRMI not to define a LearningResource as a subtype of CreativeWork. Essentially the problem comes when you try to define what is a Learning Resource. Everyone who has tried so far has come up with something like “a resource which is used in learning, education or training”. That doesn’t rule out anything. Whether a magazine like Germany’s [Spiegel](http://www.spiegel.de/) is a learning resource depends on whether you are a German speaker or an American studying German. In presentations I have compared this problem to that of defining “what is a seat”. You can get seats in all shapes and forms with many different characteristics: chairs, sofas, saddles, stools; so in the end you just have to say a seat is something you sit on. Rather than rehash the problem of deciding what is and isn’t a learning resource, we took the approach of providing a way by which people can describe the educational properties of any Creative Work.

We recognised that there are some “types” of resource that are specific for learning. You can sensibly talk about textbooks and instructional videos as being are qualitatively different to novels and the movies people watch in the cinema, without denying that novels and movies are useful in education. That’s why we have the [learningResourceType](http://schema.org/learningResourceType) property. You can think of this as describing the educational genre of the resource.

In practice there are two choices for searching for learning resources. You can search those sites that are curated collections of what someone has decided are educational resources. Or you can search for the educational properties you want. So in [our attempt at creating a Google Custom Search Engine](http://blogs.pjjk.net/phil/building-a-google-custom-search-engine-for-lrmi-tagged-pages/) we looked for the [AlignmentObject](http://schema.org/AlignmentObject). Looking for the presence of a learningResourceType would be another way. The [educationalUse](http://schema.org/educationalUse) property should likewise be a good indicator.