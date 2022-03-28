---
id: 147
title: 'LRMI examples for schema.org'
date: '2015-09-22T14:24:15+01:00'
author: 'Phil Barker'
excerpt: 'It&rsquo;s been over two years since the LRMI properties were added to schema.org. One thing that we should have done much sooner is to create simple examples of how they can be used for the schema.org website (see, for example, the bottom of the Creative Work page). We&rsquo;re nearly there. We have two examples in &hellip; <a href="http://blogs.pjjk.net/phil/lrmi-examples-for-schema-org/">Continue reading <span>LRMI examples for schema.org</span> <span>&rarr;</span></a>'
layout: post
guid: 'http://blogs.pjjk.net/phil/?p=1524'
permalink: 'http://blogs.pjjk.net/phil/lrmi-examples-for-schema-org/'
enclosure:
    - "\n\n"
syndication_source:
    - 'Sharing and learning'
syndication_source_uri:
    - 'http://blogs.pjjk.net/phil'
syndication_source_id:
    - 'http://blogs.pjjk.net/phil/feed/'
'rss:comments':
    - 'http://blogs.pjjk.net/phil/lrmi-examples-for-schema-org/#comments'
'wfw:commentRSS':
    - 'http://blogs.pjjk.net/phil/lrmi-examples-for-schema-org/feed/'
syndication_feed:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed_id:
    - '2'
syndication_permalink:
    - 'http://blogs.pjjk.net/phil/lrmi-examples-for-schema-org/'
syndication_item_hash:
    - 27b6b633c1f7f15cdb7b282da05cdb75
    - 3c8d1eeb73815cfbe6807bfd0d98fb9d
    - 3c8d1eeb73815cfbe6807bfd0d98fb9d
    - 842f85bf30edb9736b5dc168e3d43251
    - 842f85bf30edb9736b5dc168e3d43251
    - 43c172f36f987d9a6ff28c35dc890d4d
categories:
    - cetis
    - LRMI
    - schema.org
---

It’s been over two years since the [LRMI properties were added to schema.org](http://blogs.pjjk.net/phil/lrmi-in-schema/). One thing that we should have done much sooner is to create simple examples of how they can be used for the schema.org website (see, for example, the bottom of the [Creative Work](http://schema.org/CreativeWork) page). We’re nearly there.

We have two examples in the final stages of preparation, so close to ready that you can see [previews](http://philb-lrmi-examples.appspot.com/AlignmentObject) of what we propose to add (at the bottom of that page).

The first example is very simple, just a few lines describing a lesson plan for US second grade teachers (NB, the lesson plan itself is not included in the example):

```
<pre class="brush: xml; title: ; notranslate">
<div>
  <h1>Designing a treasure map</h1>
  <p>Resource type: lesson plan, learning activity</p>
  <p>Target audience: teachers</p>
  <p>Educational level: US Grade 2</p>
  <p>Location: <a href="http://example.org/lessonplan">http://example.org/lessonplan</a></p>
</div>
```

With added microdata that becomes

```
<pre class="brush: xml; title: ; notranslate">
<div itemscope itemtype="http://schema.org/CreativeWork">
    <h1 itemprop="name">Designing a treasure map</h1>
    <p>Resource type: 
      <span itemprop="learningResourceType">lesson plan</span>, 
      <span itemprop="learningResourceType">learning activity</span>
    </p>
    <p>Target audience: 
      <span itemprop="audience" itemscope itemtype="http://schema.org/EducationalAudience">
        <span itemprop="educationalRole">teacher</span></span>s.
    </p>
    <p itemprop="educationalAlignment" itemscope itemtype="http://schema.org/AlignmentObject">
        <span itemprop="alignmentType">Educational level</span>: 
        <span itemprop="educationalFramework">US Grade Levels</span> 
        <span itemprop="targetName">2</span>
        <link itemprop="targetUrl" href="http://purl.org/ASN/scheme/ASNEducationLevel/2" />
    </p>
    <p>Location: <a itemprop="url" href="http://example.org/lessonplan">http://example.org/lessonplan</a></p>
</div>
```

(Other flavours of schema.org markup are at the bottom of the [AlignmentObject preview](http://philb-lrmi-examples.appspot.com/AlignmentObject).)

This is illustrates a few points:

- free text learning resource types, which can be repeated
- the audience for the resource (teachers) is different from the grade level of the end users (pupils)
- educationalRole is a property of EducationalAudience, not the CreativeWork being described
- how the AlignmentObject should be used to specify the grade level appropriateness of the resource
- human readable grade level information is supplemented with a machine readable URI as the targetUrl

The second example is more substantial. It is based on a [resource from BBC bitesize](http://www.bbc.co.uk/education/clips/z3sjtfr) (though we have hacked the HTML around a bit). Here’s the HTML

```
<pre class="brush: xml; title: ; notranslate">
<div>
    <h1>The Declaration of Arbroath</h1>
    <p>A lesson plan for teachers with associated video. 
       Typical length of lesson, 1 hour. 
       Recommended for children aged 10-12 years old.
    </p>
    <p>Subject: Wars of Scottish independence</p>
    <p>Alignment to curriculum:</p>
    <ul>
        <li>England 
            National Curriculum: KS 3 History: The middle ages (12th to 15th century)
        </li>
        <li>Scotland 
            SCQF: Level 2
            Curriculum for Excellence: Social studies: people past events and societies: The Wars of Independence
        </li>
    </ul>
    <p>Location: <a href="http://example.org/lessonplan">http://example.org/lessonplan</a></p>
    <video>
        <source src="http://example.org/movie.mp4" type="video/mp4" />
        Duration 03:12
    </video>
</div>
```

and here’s the JSON-LD:

```
<pre class="brush: jscript; title: ; notranslate">
<script type="application/ld+json">
{
  "@context":  "http://schema.org/",
  "@type": "WebPage",
  "name": "The Declaration of Arbroath",
  "about": "Wars of Scottish independence",
  "learningResourceType": "lesson plan",
  "timeRequired": "1 hour",
  "typicalAgeRange": "10-12",
  "audience": {
      "@type": "EducationalAudience",
      "educationalRole": "teacher"
  },
  "educationalAlignment": [
    {
      "@type": "AlignmentObject",
      "alignmentType": "educationalSubject",
      "educationalFramework": " Curriculum for Excellence: ",
      "targetName": "Social studies: people past events and societies",
      "targetUrl": "http://example.org/CFE/subjects/3362"      
    },
    {
      "@type": "AlignmentObject",
      "alignmentType": "educationalLevel",
      "educationalFramework": "SCQF",
      "targetName": "Level 2",
      "targetUrl":  "http://example.org/SCQF/levels/2"      
    },
    {
      "@type": "AlignmentObject",
      "alignmentType": "educationalLevel",
      "educationalFramework": "National Curriculum",
      "targetName": "KS 3",
      "targetUrl": "http://example.org/ENC/levels/KS3"
    },
    {
      "@type": "AlignmentObject",
      "alignmentType": "educationalSubject",
      "educationalFramework": "National Curriculum",
      "targetName": "History: The middle ages (12th to 15th century)",
      "targetUrl" : "http://example.org/ENC/subjects/3102"
    }
  ],
  "url" : "http://example.org/lessonplan",
  "video": {
    "@type": "VideoObject",
    "description": "Video description",
    "duration": "03:12",
    "name": "Video Title",
    "thumbnailUrl": "http://example.org/thubnail.mp4",
    "uploadDate": "2000-01-01",
    "url" : "http://example.org/movie.mp4"
  }
}
</script>
```

(Again other flavours of schema.org markup are at the bottom of the [AlignmentObject preview](http://philb-lrmi-examples.appspot.com/AlignmentObject).)

The additional points to note here are that

- we chose to mark up the lesson plan as the learning resource rather than the video. Nothing wrong with marking up the video as a learning resource, but things like educational alignment will be more explicit for lesson plans. (Again, neither the lesson plan nor the video are in the example)
- the typical learning time of the lesson plan is not the same as the duration of the video
- this example treat the English and Scottish curricula as providing subjects for study at given educational levels. It would be possible to go deeper and align to specific competence statements (e.g. say that the alignment is that the resource “teaches” Curriculum for Excellence outcome SOC 2-01a “I can use primary and secondary sources selectively to research events in the past.”
- the educational subject (i.e. the educational context of the resource in terms of those subjects studied at school) is different from the topic that the resource is about
- it’s a shame that there are no real URIs to use for the targets of these aligments
- while you can omit the url property for the described resource, we thought it safer to include it; the default value is the URI of the webpage in which the markup is included, which may be what you need, but in the case of stand-alone JSON-LD you’re lost without an explicit value for “url”

As ever, comments would be welcome.