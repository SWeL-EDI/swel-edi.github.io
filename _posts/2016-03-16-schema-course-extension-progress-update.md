---
id: 131
title: 'Schema course extension progress update'
date: '2016-03-16T15:05:01+00:00'
author: 'Phil Barker'
excerpt: 'I am chair of the Schema Course Extension W3C Community Group, which aims to develop an extension for schema.org concerning the discovery of any type of educational course. This progress update is cross-posted from there. If the forming-storming-norming-performing model of group development still has any currency, then I am pretty sure that February was the &hellip; <a href="http://blogs.pjjk.net/phil/schema-course-extension-progress-update/">Continue reading <span>Schema course extension progress update</span> <span>&rarr;</span></a>'
layout: post
guid: 'http://blogs.pjjk.net/phil/?p=1604'
permalink: 'http://blogs.pjjk.net/phil/schema-course-extension-progress-update/'
enclosure:
    - "\n\n"
syndication_source:
    - 'Sharing and learning'
syndication_source_uri:
    - 'http://blogs.pjjk.net/phil'
syndication_source_id:
    - 'http://blogs.pjjk.net/phil/feed/'
'rss:comments':
    - 'http://blogs.pjjk.net/phil/schema-course-extension-progress-update/#respond'
'wfw:commentRSS':
    - 'http://blogs.pjjk.net/phil/schema-course-extension-progress-update/feed/'
syndication_feed:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed_id:
    - '2'
syndication_permalink:
    - 'http://blogs.pjjk.net/phil/schema-course-extension-progress-update/'
syndication_item_hash:
    - ea6cb220a9420d85d88f7974983cb354
    - 4c79aee0486205cb6c8befc730827b79
    - 4c79aee0486205cb6c8befc730827b79
    - 7b76c6a6697cee1aeb84dc9cbce4f47e
    - 7b76c6a6697cee1aeb84dc9cbce4f47e
    - d76b6232e6a5b34f4b4d8707f30e0048
categories:
    - cetis
    - 'course description'
    - LRMI
    - schema.org
---

I am chair of the [Schema Course Extension](https://www.w3.org/community/schema-course-extend/) W3C Community Group, which aims to develop an extension for schema.org concerning the discovery of any type of educational course. This progress update is cross-posted from there.

If the [forming-storming-norming-performing](https://en.wikipedia.org/wiki/Tuckman%27s_stages_of_group_development) model of group development still has any currency, then I am pretty sure that February was the “storming” phase. There was [a lot of discussion](https://lists.w3.org/Archives/Public/public-schema-course-extend/2016Feb/thread.html), much of it around the modelling of the basic entities for describing courses and how they relate to core types in schema (the [Modelling Course and CourseOffering](https://lists.w3.org/Archives/Public/public-schema-course-extend/2016Feb/thread.html#msg10) &amp; [Course, a new dawn?](https://lists.w3.org/Archives/Public/public-schema-course-extend/2016Feb/thread.html) threads). Pleased to say that the discussion did its job, and we achieved some sort of consensus (norming) around modelling courses in two parts

> **Course**, a subtype of [CreativeWork](http://schema.org/CreativeWork): A description of an educational course which may be offered as distinct instances at different times and places, or through different media or modes of study. An educational course is a sequence of one or more educational events and/or creative works which aims to build knowledge, competence or ability of learners.
> 
> **CourseInstance**, a subtype of [Event](http://schema.org/Event): An instance of a Course offered at a specific time and place or through specific media or mode of study or to a specific section of students.
> 
> **hasCourseInstance**, a property of Course with expected range CourseInstance: An offering of the course at a specific time and place or through specific media or mode of study or to a specific section of students.

(see [Modelling Course and CourseInstance](https://www.w3.org/community/schema-course-extend/wiki/Modelling_Course_and_CourseOffering) on the group wiki)

This modelling, especially the subtyping from existing schema.org types allows us to meet many of the [requirements arising from the use cases](https://www.w3.org/community/schema-course-extend/wiki/Outline_use_cases) quite simply. For example, the [cost of a course instance](https://www.w3.org/community/schema-course-extend/wiki/Cost_of_course) can be provided using the [offers](http://schema.org/offers) property of schema.org/Event.

The wiki is working to a reasonable extent as a place to record the outcomes of the discussion. Working from the [outline use cases page](https://www.w3.org/community/schema-course-extend/wiki/Outline_use_cases) you can see which requirements have pages, and those pages that exist point to the relevant discussion threads in the mail list and, where we have got this far, describe the current solution. The wiki is also the place to find [examples](https://www.w3.org/community/schema-course-extend/wiki/Examples_of_sites_with_course_information) for testing whether the proposed solution can be used to mark up real course information.

As well as the wiki, we have the [proposal on github](https://github.com/westurner/schemaorg/tree/feature/ext-course), which can be used to build working [test instances on appspot](http://course.schema-course-extend.appspot.com/) showing the proposed changes to the schema.org site.

The next phase of the work should see us performing, working through the requirements from the use cases and showing how they can be me. I think we should focus first on those that look easy to do with existing properties of schema.org/Event and schema.org/CreativeWork.