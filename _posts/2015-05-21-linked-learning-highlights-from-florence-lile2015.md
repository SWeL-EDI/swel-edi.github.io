---
id: 169
title: 'Linked learning highlights from Florence #LILE2015'
date: '2015-05-21T17:22:59+01:00'
author: 'Phil Barker'
excerpt: 'I was lucky enough to go to Florence for some of the pre WWW2015 conference workshops&nbsp;because Stefan Dietze invited me to talk at the Linked Learning workshop &ldquo;Learning &amp; Education with the Web of Data&ldquo;. Rather than summarize everything I saw I would like to give&nbsp;brief pointers to three&nbsp;presentations from that workshop and the &ldquo;Web-base &hellip; <a href="http://blogs.pjjk.net/phil/linked-learning-highlights-from-florence-lile2015/">Continue reading <span>Linked learning highlights from Florence #LILE2015</span> <span>&rarr;</span></a>'
layout: post
guid: 'http://blogs.pjjk.net/phil/?p=1378'
permalink: 'http://blogs.pjjk.net/phil/linked-learning-highlights-from-florence-lile2015/'
enclosure:
    - "\n\n"
syndication_source:
    - 'Sharing and learning'
syndication_source_uri:
    - 'http://blogs.pjjk.net/phil'
syndication_source_id:
    - 'http://blogs.pjjk.net/phil/feed/'
'rss:comments':
    - 'http://blogs.pjjk.net/phil/linked-learning-highlights-from-florence-lile2015/#comments'
'wfw:commentRSS':
    - 'http://blogs.pjjk.net/phil/linked-learning-highlights-from-florence-lile2015/feed/'
syndication_feed:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed_id:
    - '2'
syndication_permalink:
    - 'http://blogs.pjjk.net/phil/linked-learning-highlights-from-florence-lile2015/'
syndication_item_hash:
    - bfaaa1cfb6b52742932fc1a69510bfe7
categories:
    - cetis
    - 'course description'
    - 'semantic technologies'
---

![david](http://blogs.pjjk.net/phil/content/uploads/david-150x150.jpg)I was lucky enough to go to Florence for some of the pre WWW2015 conference workshops because [Stefan Dietze](https://stefandietze.wordpress.com/) invited me to talk at the Linked Learning workshop “[Learning &amp; Education with the Web of Data](https://lile2015.wordpress.com/)“. Rather than summarize everything I saw I would like to give brief pointers to three presentations from that workshop and the “Web-base Education Technologies” (WebET 2015) workshop that followed it that were personal highlights. Many thanks to Stefan for organizing the conference (and also to the Spanish company [Gnoss](http://products.gnoss.com/en/community/gnossproducts/resource/gnoss-educacion/5e34f490-3016-4277-850e-b117ca7e0e76) for sponsoring it).

## Semantic TinCan

I’ve followed the work on [Tin Can / xAPI / Experience API](http://www.adlnet.gov/capabilities/tla/experience-api.html) since its inception. Lorna and I put a section about it into our Cetis Briefing on [Activity Data and Paradata](http://publications.cetis.org.uk/2013/808), so I was especially interested in [Tom De Nies](http://users.ugent.be/~tdenies/)‘s presentation on TinCan2PROV: [Exposing Interoperable Provenance of Learning Processes Through Experience API Logs](http://www.www2015.it/documents/proceedings/companion/p689.pdf). Tin Can statements are basically elaborations of “I did this,” providing more information about the who, how and what referred to by those three words. Tom has a background in provenance metadata and saw the parallel between those statements and the recording of actions by agents more generally, and specifically with the model behind the [W3C PROV](http://www.w3.org/TR/prov-overview/) ontology for recording information about entities, activities, and people involved in producing a piece of data or thing. Showing that TinCan can be mapped to W3C PROV is of more than academic interest: the TinCan spec provides only one binding, JSON but the first step of Tom’s work was to upgrade that to JSON-LD and then through the mapping to PROV allow any of the serializations for PROV to be used (RDF/XML, N3, JSON-LD), and to bring the Tin Can statements into a format that allows them to be used by semantic technologies. Tom is hopeful that the mapping is lossless, you can try it yourself at [tincan2prov.org](http://tincan2prov.org/).

## Linking Courses

I also have an increasing interest in the semantic representation of courses, there’s some interest in adding Courses to schema.org, but also within my own department some of us would like to explore advantages of moving away from course descriptors as PDF documents to something that could be a little more connected with each other and the outside world. Fouad Zablith’s [presentation](http://www.slideshare.net/fzablith/2015050601-f-zablithlilewww2015?ref=https://twitter.com/i/cards/tfw/v1/600627974795304961?cardname=player&autoplay=true&earned=true) on [Interconnecting and Enriching Higher Education Programs using Linked Data](http://www.www2015.it/documents/proceedings/companion/p711.pdf) was like seeing the end point of that second line of interest. The data model Fouad uses combines a model of a course with information about the concepts taught and the learning materials used to teach them. Course information is recorded using [Semantic MediaWiki](https://semantic-mediawiki.org/) to produce both human readable and linked data representations of the courses across a program of study. A bookmarklet allows information about resources that are useful for these courses to be added to the graph–but importantly attached via the concept that is studied, and so available to students of any course that teaches that concept. Finally, on the topic of several courses teaching the same concepts, sometimes such repetition is deliberate, but sometimes it is unwanted.

<figure class="wp-caption aligncenter" id="attachment_1381" style="width: 579px">[![Showing which concepts (middle) from one course (left) occur in other courses (right). Image from Fouad Zablith's presentation (see link in text)](http://blogs.pjjk.net/phil/content/uploads/Picture1-579x480.png)](http://blogs.pjjk.net/phil/content/uploads/Picture1.png)<figcaption class="wp-caption-text">Showing which concepts (middle) from one course (left) occur in other courses (right). Image from Fouad Zablith’s presentation (see link in text)</figcaption></figure>Fouad showed how analysis of the concept – course part of the graph could be useful it surfacing cases of where there were perhaps too many concepts in a course that had been previously covered elsewhere (see image, above)

## Linking Resources

One view of a course (that makes especial sense to anyone who thinks about etymology) is that it is a learning pathway, and one view of a pathway is as an [Directed Acyclic Graph](http://en.wikipedia.org/wiki/Directed_acyclic_graph), i.e. an ordered route through a series of resources. In the WebET workshop, [Andrea Zielinski](http://www.iosb.fraunhofer.de/servlet/is/46293/) presented [A Case Study on the Use of Semantic Web Technologies for Learner Guidance ](http://www.www2015.it/documents/proceedings/companion/p1425.pdf)which modelled such a learning pathway as a directed graph and represented this graph using [OWL 2 DL](http://www.w3.org/TR/owl2-primer/#OWL_2_DL_and_OWL_2_Full). The conclusion to her paper says “The approach is applicable in the Semantic Web context, where distributed resources often are already annotated according to metadata standards and various open-source domain and user ontologies exist. Using the reasoning framework, they can be sequenced in a meaningful and user-adaptive way.” But at this stage the focus is on showing that the expressivity of OWL 2 DL is enough to represent a learning pathway and testing the efficiency of querying such graphs.