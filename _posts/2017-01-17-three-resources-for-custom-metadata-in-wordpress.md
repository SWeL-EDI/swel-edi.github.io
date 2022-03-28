---
id: 467
title: 'Three resources for custom metadata in WordPress'
date: '2017-01-17T11:10:34+00:00'
author: 'Phil Barker'
excerpt: "<p>When developing WordPress for use as a CMS one&nbsp;approach I have used is to create a custom post type for each type of resource and custom metadata&nbsp;boxes for relevant properties of those types. &nbsp;I&rsquo;ve used that approach when exploring the possibility of using&nbsp;WordPress as a semantic web platform to edit schema.org metadata, when building course &hellip; <a href=\"https://blogs.pjjk.net/phil/resources-custom-metadata-in-wordpress/\">Continue reading <span>Three resources for custom metadata in WordPress</span> <span>&rarr;</span></a></p>\n<p>The post <a rel=\"nofollow\" href=\"https://blogs.pjjk.net/phil/resources-custom-metadata-in-wordpress/\">Three resources for custom metadata in WordPress</a> appeared first on <a rel=\"nofollow\" href=\"https://blogs.pjjk.net/phil\">Sharing and learning</a>.</p>"
layout: post
guid: 'https://blogs.pjjk.net/phil/?p=1715'
permalink: 'https://blogs.pjjk.net/phil/resources-custom-metadata-in-wordpress/'
enclosure:
    - "\n\n"
syndication_source:
    - 'Sharing and learning'
syndication_source_uri:
    - 'https://blogs.pjjk.net/phil'
syndication_source_id:
    - 'http://blogs.pjjk.net/phil/feed/'
'rss:comments':
    - 'https://blogs.pjjk.net/phil/resources-custom-metadata-in-wordpress/#respond'
'wfw:commentRSS':
    - 'https://blogs.pjjk.net/phil/resources-custom-metadata-in-wordpress/feed/'
syndication_feed:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed_id:
    - '2'
syndication_permalink:
    - 'https://blogs.pjjk.net/phil/resources-custom-metadata-in-wordpress/'
syndication_item_hash:
    - 329e2a51068451e85bb0c460313cb428
categories:
    - Other
    - 'semantic technologies'
    - WordPress
---

When developing WordPress for use as a CMS one approach I have used is to create a [custom post type](https://codex.wordpress.org/Post_Types) for each type of resource and custom metadata boxes for relevant properties of those types. I’ve used that approach when exploring the possibility of using [WordPress as a semantic web platform](https://blogs.pjjk.net/phil/wordpress-as-a-semantic-web-platform/) to edit schema.org metadata, when building course information pages for students and am doing so again in updating some work I did on [WordPress as a lightweight repository](https://blogs.pjjk.net/phil/cetis-publications-now-on-wordpress/). Registering a custom post type is pretty straightforward, follow the example in the codex page, I found handling custom metadata boxes a little more difficult. Here are three resources that helped.

## Doing it long hand

It’s a few years old, but I found Justin Tadlock’s Smashing Magazine article ***[How To Create Custom Post Meta Boxes In WordPress](https://www.smashingmagazine.com/2011/10/create-custom-post-meta-boxes-wordpress/)*** really useful as a clear and informative tutorial. It was invaluable in understanding how metaboxes work. If I had only wanted one or two simple text custom metadata fields then coding them myself would be an option, but I found a couple of problems. Firstly, I was repeating the same code too many times. Secondly when I thought about wanting to store dates or urls or links to other posts, with suitable user interface elements and data validation, I could see the amount of code needed was only going to increase. So I looked to see whether any better programmers than I had created anything I could use.

## Using a helper plugin

I found two plugins that promised to provide a framework to simplify the creation of metaboxes. These are not plugins that provide anything that the end user can see directly, rather they provide functions that can be used in theme an plugin development. They both reduce the work of creating a metabox down to creating an array with the properties you want the metabox to have. They both introduce a dependency on code I cannot maintain, which is something I am always cautious about in using third-party plugins, but it’s much more viable than the alternative of creating such code from scratch and maintaining it myself.

***[CMB2](https://en-gb.wordpress.org/plugins/cmb2/)*** is “a metabox, custom fields, and forms library for WordPress that will blow your mind.” It is free and open source, with development [hosted on GitHub](https://github.com/WebDevStudios/CMB2/). It seems quite mature (version 1.0 was in Nov 2013), with a large installation base and decent amount of current activity on github.

***[Meta Box](https://en-gb.wordpress.org/plugins/meta-box/)*** is “a powerful, professional developer toolkit to create custom meta boxes and custom fields for WordPress.” It too is free and released under GPL2 licence, but there are paid-for extensions (also GPL2 licensed) and I don’t see any open source development (I may not have looked in the right place). Meta box has been around for a couple of years, is regularly updated and has a very large user base. The [paid-for extensions](https://metabox.io/plugins/) give me some hope that the developers have a sustainable business model, but a worry that maybe ‘free’ doesn’t include the one function that at sometime I will really need. Well, developers cannot live on magic beans so I wouldn’t mind paying.

In the end both plugins worked well, but Meta Box allows the creation of custom fields for a link from one post to another, which I didn’t see in CMB2. That’s what I need for a metadata field to say that the author of the book described in one post is a person described in another.

The post [Three resources for custom metadata in WordPress](https://blogs.pjjk.net/phil/resources-custom-metadata-in-wordpress/) appeared first on [Sharing and learning](https://blogs.pjjk.net/phil).