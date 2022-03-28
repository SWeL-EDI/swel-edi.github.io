---
id: 484
title: 'Requirements for online exam system'
date: '2017-03-21T10:41:44+00:00'
author: 'Phil Barker'
excerpt: "<p>Some time back we started looking for an online exam system for some of our computer science exams. Part of the process was to list a set of &ldquo;acceptance criteria,&rdquo; i.e. conditions that any system we looked at had to meet. One of my aims in writing these was to &nbsp;avoid chasing after some mythical &hellip; <a href=\"https://blogs.pjjk.net/phil/requirements-online-exam-system/\">Continue reading <span>Requirements for online exam system</span> <span>&rarr;</span></a></p>\n<p>The post <a rel=\"nofollow\" href=\"https://blogs.pjjk.net/phil/requirements-online-exam-system/\">Requirements for online exam system</a> appeared first on <a rel=\"nofollow\" href=\"https://blogs.pjjk.net/phil\">Sharing and learning</a>.</p>"
layout: post
guid: 'https://blogs.pjjk.net/phil/?p=1733'
permalink: 'https://blogs.pjjk.net/phil/requirements-online-exam-system/'
enclosure:
    - "\n\n"
syndication_source:
    - 'Sharing and learning'
syndication_source_uri:
    - 'https://blogs.pjjk.net/phil'
syndication_source_id:
    - 'http://blogs.pjjk.net/phil/feed/'
'rss:comments':
    - 'https://blogs.pjjk.net/phil/requirements-online-exam-system/#respond'
'wfw:commentRSS':
    - 'https://blogs.pjjk.net/phil/requirements-online-exam-system/feed/'
syndication_feed:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed_id:
    - '2'
syndication_permalink:
    - 'https://blogs.pjjk.net/phil/requirements-online-exam-system/'
syndication_item_hash:
    - 2d11b24e7e47376d38937774d7648683
categories:
    - Other
---

Some time back we started looking for an online exam system for some of our computer science exams. Part of the process was to list a set of “acceptance criteria,” i.e. conditions that any system we looked at had to meet. One of my aims in writing these was to avoid chasing after some mythical ‘perfect’ system, and focus on finding one that would meet our needs. Although the headings below differ, as a system for high stakes assessment the overarching requirements were security, reliability, scalability, which are reflected below.

Having these criteria were useful in reaching a consensus decision when there was no ‘perfect’ system.

## Security:

- Only authorised staff (+ external examiners) to have access before exam time.
- Only authorised staff and students to have access during exams.
- Only authorised staff (+ external examiners) to have access to results.
- Authorised staff and external examiners to have only the level of access they need, no more.
- Software must be kept up-to-date and patched in a timely fashion
- Must track and report all access attempts
- Must not rely on security by obscurity.
- Secure access must not depend on location.

## Audit:

- Provide suitable access to internal checkers and external examiners.
- Logging of changes to questions and exams would be desirable.
- It must be possible to set a point after which exams cannot be changed (e.g. once they are passed by checkers)
- Must be able to check marking (either exam setter or other individual), i.e. provide clear reports on how each question was answered by each candidate.
- Must be possible to adjust marking/remark if an error is found after the exam (e.g. if a mistake was made in setting the correct option for mcq, or if question was found to be ambiguous or too hard)

## Pedagogy:

- <del>Must should be possible to reproduce content of previous CS electronic exams in similar or better format</del> \[this one turned out not to be important\]
- Must be able to decide how many points to assign to each question
- Desirable to have provision for alternate answers or insignificant difference in answers (e.g. y=a\*b, y=b\*a)
- Desirable to reproduce style of standard HW CS exam papers, i.e. four potentially multipart questions, with student able to choose which 3 to answer
- Desirable to be possible to provide access to past papers on formative basis
- Desirable to support formative assessment with feedback to students
- Must be able to remove access to past papers if necessary.
- Students should be able to practice with same (or very similar) system prior to exam
- Desirable to be able to open up access to a controlled list of websites and tools (c.f. open book exams)
- Should be able to use mathematical symbols in questions and answers, including student entered text answers.

## Operational

- Desirable to have programmatic transfer of staff information to assessment system (i.e. to know who has what role for each exam)
- Must be able to transfer student information from student information system to assessment system (who sits which exam and at which campus).
- Desirable to be able to transfer study requirements from student information system to assessment system (e.g. who gets extra time in exams)
- Programmatic transfer student results from assessment system to student record systems or VLE (one is required)
- Desirable to support import/export of tests via QTI.
- Integration with VLE for access to past papers, mock exams, formative assessment in general (e.g. IMS LTI)
- Hardware &amp; software requirements for test taking must be compatible with PCs we have (at all campuses and distance learning partners).
- Set up requirements for labs in which assessments are taken must be within capabilities of available technical staff at relevant centre (at all campuses and distance learning partners).
- Lab infrastructure\* and servers must be able to operate under load of full class logging in simultaneously (\* at all campuses and distance learning partners)
- Must have adequate paper back up at all stages, at all locations
- Must be provision for study support exam provision (e.g. extra time for some students)
- Need to know whether there is secure API access to responses.
- API documentation must be open and response formats open and flexible.
- Require support helpline / forum / community.
- Timing of release of encryption key

## **Other**

- **Costs**. Clarify how many students would be involved, what this would cost.

The post [Requirements for online exam system](https://blogs.pjjk.net/phil/requirements-online-exam-system/) appeared first on [Sharing and learning](https://blogs.pjjk.net/phil).