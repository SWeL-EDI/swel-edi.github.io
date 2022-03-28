---
id: 167
title: 'LRMI / schema.org validation'
date: '2015-05-27T15:39:58+01:00'
author: 'Phil Barker'
excerpt: 'We are currently preparing some examples of LRMI metadata.&nbsp;While these are intended to be informative only, we know that they will affect implementations more than any normative text we could put into a spec&ndash;I mean what developer reads the spec when you can just copy an example? &nbsp;So it&rsquo;s important that the examples are valid, &hellip; <a href="http://blogs.pjjk.net/phil/lrmi-schema-org-validation/">Continue reading <span>LRMI / schema.org validation</span> <span>&rarr;</span></a>'
layout: post
guid: 'http://blogs.pjjk.net/phil/?p=1387'
permalink: 'http://blogs.pjjk.net/phil/lrmi-schema-org-validation/'
enclosure:
    - "\n\n"
syndication_source:
    - 'Sharing and learning'
syndication_source_uri:
    - 'http://blogs.pjjk.net/phil'
syndication_source_id:
    - 'http://blogs.pjjk.net/phil/feed/'
'rss:comments':
    - 'http://blogs.pjjk.net/phil/lrmi-schema-org-validation/#comments'
'wfw:commentRSS':
    - 'http://blogs.pjjk.net/phil/lrmi-schema-org-validation/feed/'
syndication_feed:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed_id:
    - '2'
syndication_permalink:
    - 'http://blogs.pjjk.net/phil/lrmi-schema-org-validation/'
syndication_item_hash:
    - a4177e029e161f3b638b30f50f84f58e
categories:
    - cetis
    - LRMI
    - schema.org
---

We are currently preparing some examples of LRMI metadata. While these are intended to be informative only, we know that they will affect implementations more than any normative text we could put into a spec–I mean what developer reads the spec when you can just copy an example? So it’s important that the examples are valid, and that set me to pulling together a list of tools &amp; services useful for validating LRMI, and by extension schema.org.

Common things to test for:

- simple syntax errors produced by typos, not closing tags and so on.
- that the data extracted is valid schema.org / LRMI
- using properties that don’t belong to the stated resource type, e.g. educationalRole should be a property of EducationalAudience not of CreativeWork.
- loose or strict interpretation of expected value types, e.g. the author property should have a Person or Organization as its value, dates and times should be in iso 8601 format?
- is the data provided for properties from the value space they should be? i.e. does the data provider use the controlled vocabulary you want?
- check that values are provided for properties you especially require

\[**Hint**, if it is the last two that you are interested in then you’re out of luck for now, but do skip to the “want more” section at the end.\]

See also [Structured Data Markup Visualization, Validation and Testing Tools](http://www.seoskeptic.com/structured-data-markup-validation-testing-tools/) by Jarno van Driel and Aaron Bradley.

## Schema.org testing tools

### Google structured data testing tool

[https://developers.google.com/structured-data/testing-tool/ ](https://developers.google.com/structured-data/testing-tool/)

If Google is your target this is as close to definitive as you can get. You can validate code on a server via a URL or by copying and pasting it into a text window, in return you get a formatted view of the data Google would extract.

**Validates:** HTML + microdata, HTML + RDFa, JSON-LD

**Downsides:** it used to be possible to pass the URL of the code to be validated as a query parameter appended to the testing tool URL and thus create a “validate this page” link, but that no longer seems to be the case.

Also, the testing tool reproduces Google’s loose interpretation of the spec, and will try to make the best sense it can of data that isn’t strictly compliant. So where the author of a creative work is supposed to be a schema.org/Person if you supply text, the validator will silently interpret that text as the name of a Person entity. Also dates not in ISO 8601 format get corrected (October 4 2012 becomes 2012-10-4 That’s great if your target is as forgiving as Google, but otherwise might cause problems.

But the biggest problem seems to be that pretty much any syntactically valid JSON-LD will validate.

### Yandex structured data validator

<https://webmaster.yandex.com/microtest.xml>

Similar to the Google testing tool, but with slightly larger scope (validates OpenGraph and microformats as well as schema). Not quite as forgiving as Google, a date in format October 4 2012 is flagged as an error, and while text is accepted as a value for author it is not explicitly mapped to the author’s name.

**Validates:** HTML + microdata, HTML + RDFa, JSON-LD

**Downsides:** because the tool is designed to validate raw RDF / JSON-LD etc, just because something validates does not mean that it is valid schema.org mark up. For example, this JSON-LD validates:

```
{ "@context": [
    { 
         "@vocab": "http://Schema.org/"
    }
 ],
     "@type": "CreativeWork" ,
     "nonsense" : "Validates"
 }
```

Unlike the Google testing tool you do get an appropriate error message if you correct the @vocab URI to have a lower-case S, making this the best JSON-LD validator I found.

### Bing markup validator

<http://www.bing.com/toolbox/markup-validator>

“Verify the markup that you have added to your pages with Markup Validator. Get an on-demand report that shows the markup we’ve discovered, including HTML Microdata, Microformats, RDFa, Schema.org, and OpenGraph. To get started simply sign in or sign up for Bing Webmaster Tools.”

**Downsides:** requires registration and signing-in so I didn’t try it.

### schema.org highlighter

[http://www.curriki.org/xwiki/bin/view/Coll\_jmarks/LRMIViewerBookmarkTool](http://www.curriki.org/xwiki/bin/view/Coll_jmarks/LRMIViewerBookmarkTool)

A useful feature of the validators listed above is that they produce something that is human readable. If you would like this in the context of the webpage, Paul Libbrecht has made a highlighter, a little bookmarklet that transforms the schema.org markup into visible paragraphs one can visually proof.

## Translators and other parsers

Not validators as such, but the following will attempt to read microdata, RDFa or JSON-LD and so will complain if there are errors. Additionally they may provide human readable translations that make it easier to spot errors.

### RDF Translator

<http://rdf-translator.appspot.com/>

“RDF Translator is a multi-format conversion tool for structured markup. It provides translations between data formats ranging from RDF/XML to RDFa or Microdata. The service allows for conversions triggered either by URI or by direct text input. Furthermore it comes with a straightforward REST API for developers.” …and of course is your data isn’t valid it won’t translate.

**Validates** pretty much any RDF / microdata format you care to name, either by entering text in a field or by reference via a URI.

**Downsides:** again purely syntactic checking, doesn’t check whether the code is valid schema.org markup.

### Structured data linter

<http://linter.structured-data.org/>

Produces a nicely formatted, human readable representation of structured data.

**Validates**: HTML + microdata, HTML + RDFa either by URL, file upload or direct input.

**Downsides:** another that is purely syntactic.

### JSON-LD Playground

<http://json-ld.org/playground/>

A really useful tool for automatically simplifying or complexifying JSON-LD, but again only checks for syntactic validity.


### Nav-North LR data

<https://github.com/navnorth/LR-Data>

“A Tool to help import the content of the Learning Registry into a data store of your choice” I haven’t tried this but it does attempt to parse JSON-LD so you would expect it to complain if the code doesn’t parse.

## Want more?

The common shortcoming (for this use case anyway, all the tools are good at what they set out to do) seems to be validating whether the data extracted is actually valid schema.org or LRMI. If you want to validate against some application profile, say insisting that the licence information must be provided, or that values for learningResourceType come from some specified controlled vocabulary then you are in territory that none of the above tools even tries to cover. This is, however, in the scope of the [W3C RDF Data Shapes Working Group](http://www.w3.org/2014/data-shapes/wiki/Main_Page) “*Mission: produce a W3C Recommendation for describing structural constraints and validate RDF instance data against those.”*

A colleagues at Heriot-Watt has had students working (with input from Eric Pud’Hommeaux) on [Validata ](http://shextool.eu/#)“an intuitive, standalone web-based tool to help building valid RDF documents by validating against preset schemas written in the Shape Expressions (ShEx) language.” It is currently set up to work to validate linked data against some pre-set application profiles used in the pharmaceuticals industry. With all the necessary caveats about it being student work, no longer supported, using an approach that is preliminary to the W3C working group, this illustrates how instance validation against a description of an application profile would work.