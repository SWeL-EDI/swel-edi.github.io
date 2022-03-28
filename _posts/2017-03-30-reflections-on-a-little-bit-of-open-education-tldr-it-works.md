---
id: 502
title: 'Reflections on a little bit of open education (TL;DR: it works).'
date: '2017-03-30T08:19:06+01:00'
author: 'Phil Barker'
excerpt: "<p>We are setting up a new honours degree programme which will involve use of online resources for work based blended learning. I was asked to demonstrate some the resources and approaches that might be useful. This is one of the quick examples that I was able to knock up(*) and some reflections on how Open &hellip; <a href=\"https://blogs.pjjk.net/phil/reflections-on-a-little-bit-of-open-education-tldr-it-works/\">Continue reading <span>Reflections on a little bit of open education (TL;DR: it works).</span> <span>&rarr;</span></a></p>\n<p>The post <a rel=\"nofollow\" href=\"https://blogs.pjjk.net/phil/reflections-on-a-little-bit-of-open-education-tldr-it-works/\">Reflections on a little bit of open education (TL;DR: it works).</a> appeared first on <a rel=\"nofollow\" href=\"https://blogs.pjjk.net/phil\">Sharing and learning</a>.</p>"
layout: post
guid: 'https://blogs.pjjk.net/phil/?p=1745'
permalink: 'https://blogs.pjjk.net/phil/reflections-on-a-little-bit-of-open-education-tldr-it-works/'
enclosure:
    - "\n\n"
syndication_source:
    - 'Sharing and learning'
syndication_source_uri:
    - 'https://blogs.pjjk.net/phil'
syndication_source_id:
    - 'http://blogs.pjjk.net/phil/feed/'
'rss:comments':
    - 'https://blogs.pjjk.net/phil/reflections-on-a-little-bit-of-open-education-tldr-it-works/#respond'
'wfw:commentRSS':
    - 'https://blogs.pjjk.net/phil/reflections-on-a-little-bit-of-open-education-tldr-it-works/feed/'
syndication_feed:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed_id:
    - '2'
syndication_permalink:
    - 'https://blogs.pjjk.net/phil/reflections-on-a-little-bit-of-open-education-tldr-it-works/'
syndication_item_hash:
    - ae0ae594af33a83430a7869672f56d5d
categories:
    - annotation
    - 'Design for Online Learning'
    - 'MACS enhancement'
    - oer
    - 'open education'
    - Praxis
    - ukoer
    - WordPress
---

We are setting up a new honours degree programme which will involve use of online resources for work based blended learning. I was asked to demonstrate some the resources and approaches that might be useful. This is one of the quick examples that I was able to knock up(\*) and some reflections on how Open Education helped me. By the way, I especially like the last bit about “open educational practice”. So if the rest bores you, just skip to the end.

(\*Disclaimer: this really is a quickly-made example, it’s in no way representative of the depth of content we will aim for in the resources we use.)

## Making the resource

I had decided that I wanted to show some resources that would be useful for our first year, first semester Praxis course. This course aims to introduce students to some of the skills they will need to study computer science, ranging from appreciating the range of topics they will study to being able to use our Linux systems, from applying study skills to understanding some requirements of academic writing. I was thinking that much of this would be fairly generic and must be covered by a hundred and one existing resources when I saw this tweet:

> ‘Why Critique Research?’ Newly developed RLO from [@UoN\_SHS](https://twitter.com/UoN_SHS) HELM <https://t.co/Bh79gLXOvK> [\#elearning](https://twitter.com/hashtag/elearning?src=hash) [\#research](https://twitter.com/hashtag/research?src=hash) [\#ukoer](https://twitter.com/hashtag/ukoer?src=hash) [\#oer](https://twitter.com/hashtag/oer?src=hash) [@UniofNottingham](https://twitter.com/UniofNottingham) [pic.twitter.com/552zW8Uc4v](https://t.co/552zW8Uc4v)
> 
> — UoN HELM (@UoN\_HELM) [March 22, 2017](https://twitter.com/UoN_HELM/status/844463538676678656)

<script async="" charset="utf-8" src="https://platform.twitter.com/widgets.js"></script>

That seemed to be in roughly the right area, so I took a look at the University of Nottingham’s [HELM Open](http://www.nottingham.ac.uk/helmopen/index.php/pages/view/about) site and found an [Introduction to Referencing](http://www.nottingham.ac.uk/nursing/sonet/rlos/studyskills/referencing/). Bingo. The content seemed appropriate, but I wasn’t keen on a couple of things. First, breaking up the video in 20sec chunks I fear would mean the student spend more time ‘interacting’ with the Next-&gt; button than thinking about the content. Second, it seems a little bit too delivery oriented, I would like the student to be a little more actively engaged.

I noticed there is a little download arrow on each page which let me download the video. So I downloaded them all and used [OpenShot ](http://www.openshot.org/)to string them together into one file. I exported this and used the [h5p](https://h5p.org/) WordPress plugin to show how it could be combined with some interactive elements and hosted on a WordPress site with the [hypothes.is annotation](https://hypothes.is/) plugin, to get [this](http://pjjk.net/h5p/level-1/praxis-level-1/reference/introduction-to-referencing/):

<figure class="wp-caption aligncenter" id="attachment_1752" style="width: 497px">[![](https://blogs.pjjk.net/phil/content/uploads/introToRefs-497x480.png)](http://pjjk.net/h5p/level-1/praxis-level-1/reference/introduction-to-referencing/)<figcaption class="wp-caption-text">The remixed resource: on the top left is the video, below that some questions to prompt the students to pay attention to the most significant points, and on the right the hypothes.is pop-out for discussion.</figcaption></figure>## How openness helps

So that was easy enough, a demo of the type of resource we might produce, created in less than an afternoon. How did “openness” help make it easy.

### Open licensing and the 5Rs

[David Wiley’s famous 5Rs](http://opencontent.org/definition/) define open licences as those that let you Reuse, Revise, Remix, Retain and Redistribute learning resources. The original resource was licensed as CC:BY-NC and so permitted all of these actions. How did they help?

**Reuse**: I couldn’t have produced the video from scratch without learning some new skills or having sizeable budget, and having much more time.

**Revise**: I wasn’t happy with the short video / many page turns approach, but was able to revise the video to make it play all the way through in one go.

**Remix**: The video was then added to some formative exercises, and discussion facility added.

**Retain**: in order for us to rely on these resources when teaching we need to be sure that the resource remains available. That means taking responsibility keeping it available. Hence we’ll be hosting it on a site we control.

**Redistribute**: we will make our version available to other. This isn’t just about “paying forward”, it’s about the benefits that working in an open network being, see the discussion about nebulous open education below.

One point to make here: the licence has a Non-Commercial restriction. I understand why some people favour this, but imagine if I were an independent consultant brought in to do this work, and charged for it. Would I then be able to use the HELM material? The [recent case](https://arstechnica.co.uk/tech-policy/2017/02/creative-commons-noncommercial-licence-fedex/) about a commercial company charging to duplicate CC-licensed material for schools, which a US judge ruled within the terms of the licence might apply, but photocopying seems different to remixing. To my mind, the NC clause just complicates things too much.

### Open standards, and open source

I hadn’t heard much about David Wiley’s [ALMS framework](http://opencontent.org/definition/) for technical choices to facilitate openness (same page as before, just scroll a bit further) but it deals directly with issues I am very familiar with. Anyone who thinks about it will realise that a copy-protected PDF is not open no matter what the licence on it says. The ALMS framework breaks the reasoning for this down to four aspects: Access to editing tools, Level of expertise required, Meaningfully editable, Self sources. Hmmm. Maybe sometimes it’s clearer not to force category names into acronyms? Anyway, here’s how these helped.

**Self-sourced**, meaning the distribution format is the source code. This is especially relevant as the reason HELM sent the tweet that alerted me to their materials was that they are re-authoring material from Flash to HTML5. Aside from modern browser support, one big advantage of them doing this is that instead of having an impenetrable SWF package I had access to the assets that made the resource, notably the video clips.

**Meaningfully editable**: that access to the assets meant that I could edit the content, stringing the videos together, copying and pasting text from the transcript to use as questions.

**Level of expertise required**: I have found all the tools and services used (OpenShot, H5P, hypothes.is, WordPress) relatively easy to use, however some experience is required, for example to be familiar with various plugins available for WordPress and how to install them. Video editing in particular takes some expertise. It’s probably something that most people don’t do very often (I don’t). Maybe the general level of digital literacy level we should now aim for is one where people are familiar with photo and video editing tools as well as text oriented word processing and presentation tools. However, I’m inclined to think that the details of using the H264 video codec and AAC audio codec, packaged in a MPEG-4 Part 14 container (compare and contrast with VP9 and ogg vorbis packaged in a profile of Matroska) should remain hidden from most people. Fortunately, standardisation means that the number of options is less than it would otherwise be, and it was possible to find many pages on the web with guidance on the browser compatibility of these options (MP4 and WebM respectively).

**Access to editing tools**, where access starts with low cost. All the tools used were free, most were open source, and all ran on Ubuntu (most can also run on other platforms).

It’s notable that all these ultimately involve open source software and open standards, and work especially well when then “open” for open standards includes free to implement. That complicated bit around MP4 &amp; WebM video formats, that comes about because royalty requirements for those implementing MP4.

### Open educational practice: nebulous but important.

Open education includes but is more than open education resources, open content, open licensing and open standards. It also means talking about what we do. It means that I found out about HELM because they were openly tweeting about their resources. I think that is how I learnt about nearly all the tools discussed here ina similar manner. Yes, “pimping your stuff” is importantly open. Open education also means asking questions and writing how-to articles that let non-experts like me deal with complexities like video encoding.

There’s a deeper open education at play here as well. See that resource from HELM that I started with? It started life in the RLO CETL, i.e. in a publicly funded initiative, now long gone. And the reason I and others in the UKHE know about Creative Commons and David Wiley’s analysis of open content, that largely comes down to #UKOER, again a publicly funded initiative. UKOER and the stuff about open standards and open source was supported by Jisc, publicly funded. Alumni from these initiatives are to be found all over UKHE, through which these initiatives continue to be crucially important in building our capability and capacity to support learners in new and innovative settings.

The post [Reflections on a little bit of open education (TL;DR: it works).](https://blogs.pjjk.net/phil/reflections-on-a-little-bit-of-open-education-tldr-it-works/) appeared first on [Sharing and learning](https://blogs.pjjk.net/phil).