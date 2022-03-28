---
id: 273
title: 'Schema course extension update'
date: '2016-09-19T12:44:28+01:00'
author: 'Phil Barker'
excerpt: 'This progress update on the work to extend&nbsp;schema.org to support&nbsp;the discovery of any type of educational course is cross-posted from the Schema Course Extension W3C Community Group. If you are interested in this work please head over there. What aspects of a course can we now describe? As a result of work so far addressing &hellip; <a href="http://blogs.pjjk.net/phil/schema-course-extension-update/">Continue reading <span>Schema course extension update</span> <span>&rarr;</span></a>'
layout: post
guid: 'http://blogs.pjjk.net/phil/?p=1616'
permalink: 'http://blogs.pjjk.net/phil/schema-course-extension-update/'
enclosure:
    - "\n\n"
syndication_source:
    - 'Sharing and learning'
syndication_source_uri:
    - 'http://blogs.pjjk.net/phil'
syndication_source_id:
    - 'http://blogs.pjjk.net/phil/feed/'
'rss:comments':
    - 'http://blogs.pjjk.net/phil/schema-course-extension-update/#respond'
'wfw:commentRSS':
    - 'http://blogs.pjjk.net/phil/schema-course-extension-update/feed/'
syndication_feed:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed_id:
    - '2'
syndication_permalink:
    - 'http://blogs.pjjk.net/phil/schema-course-extension-update/'
syndication_item_hash:
    - 7668efedb6ee69d7b3784fb091b2f1c9
    - ca6215960761400701404128fe06483e
    - ca6215960761400701404128fe06483e
    - d9bf7ea3b8e1e33564a313d46c9ebf4f
    - d9bf7ea3b8e1e33564a313d46c9ebf4f
    - 8acaa6f24c29ce07b18e4e1def7925d7
    - 3a0e196feaf70f8814a8ff4c8d6c7c71
    - 3a0e196feaf70f8814a8ff4c8d6c7c71
    - 3a0e196feaf70f8814a8ff4c8d6c7c71
    - 3a0e196feaf70f8814a8ff4c8d6c7c71
    - 0701fc5521b9d94a5b72b017e4caf2e5
    - 0701fc5521b9d94a5b72b017e4caf2e5
categories:
    - 'course description'
    - LRMI
    - schema.org
    - 'semantic technologies'
---

This progress update on the work to extend schema.org to support the discovery of any type of educational course is cross-posted from the [Schema Course Extension W3C Community Group](https://www.w3.org/community/schema-course-extend/). If you are interested in this work please head over there.

**What aspects of a course can we now describe?**  
As a result of work so far addressing the [use cases that we outlined](https://www.w3.org/community/schema-course-extend/wiki/Outline_use_cases), we now have answers to the following questions about how to describe courses using schema.org:

- How to [define something as being about a course or being about an instance of that course](https://www.w3.org/community/schema-course-extend/wiki/Modelling_Course_and_CourseOffering)
- How to mark up the [identifier used by providers to identify their courses](https://www.w3.org/community/schema-course-extend/wiki/Identifying_courses_by_provider_and_code)
- How to [identify a course by provider and name](https://www.w3.org/community/schema-course-extend/wiki/Identifying_courses_by_provider_and_name)
- How to mark up the [subject of a course](https://www.w3.org/community/schema-course-extend/wiki/Subject_of_Course)
- How to identify the [location where a course is offered](https://www.w3.org/community/schema-course-extend/wiki/Location_of_a_course)
- How to identify the [start and end of an instance of a course](https://www.w3.org/community/schema-course-extend/wiki/Start_and_end_of_Course), and the [times of events that are part of it](https://www.w3.org/community/schema-course-extend/wiki/Identifying_when_course_events_happen)
- Related to start and end dates of a course, how to specify the [duration and amount of time typically required to complete a course](https://www.w3.org/community/schema-course-extend/wiki/The_typical_learning_time_or_duration_of_the_course)
- How to identify the [organizations providing and offering courses](https://www.w3.org/community/schema-course-extend/wiki/Organizations_providing_and_offering_course) (and how these two roles may differ).
- How to identify [the teacher / instructor of a course](https://www.w3.org/community/schema-course-extend/wiki/Instructor_of_a_course_instance) (who may or nay not be the creator of the course).
- How to mark up the [mode of study or delivery](https://www.w3.org/community/schema-course-extend/wiki/Mode_of_study_or_delivery#Proposal).
- How to identify a course which is a prerequisite of the course being described or to link to or describe other prerequisites.


As with anything in schema.org, many of the answers proposed are not the final word on all the detail required in every case, but they form a solid basis that I think will be adequate in many instances.

**What new properties are we proposing?**  
In short, remarkably few. Many of the aspects of a course can be described in the same way as for other creative works or events. However we did find that we needed to create two new types [Course](http://webschemas.org/Course) and [CourseInstance](http://webschemas.org/CourseInstance) to identify whether the description related to a course that could be offered at various times or a specific offering or section of that course. We also found the need for three new properties for Course: [courseCode](http://webschemas.org/courseCode), [coursePrerequisites](http://webschemas.org/coursePrerequisites) and [hasCourseInstance](http://webschemas.org/hasCourseInstance); and two new properties for CourseInstance: [courseMode](http://webschemas.org/courseMode) and [instructor](http://webschemas.org/instructor).

There are others under discussion, but I highlight these as proposed because they are **being put forward for inclusion in the next release of the schema.org** core vocabulary.

![showing how Google will display information about courses in a search gallery](https://developers.google.com/search/docs/guides/images/search-gallery-courses.png)**More good news:**  the [Google search gallery](https://developers.google.com/search/docs/guides/search-gallery) documentation for developers already includes information on how to provide the most basic info about [Courses](https://developers.google.com/search/docs/guides/search-gallery#courses). This is where we are going ![🙂](https://s.w.org/images/core/emoji/2/72x72/1f642.png)