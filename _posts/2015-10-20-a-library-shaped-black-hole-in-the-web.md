---
id: 141
title: 'A library shaped black hole in the web?'
date: '2015-10-20T14:26:47+01:00'
author: 'Phil Barker'
excerpt: 'A library shaped black hole in the web? was the name of an OCLC event that was getting its second(?) run in Edinburgh last week, looking at how libraries can contribute to the web, using new technologies (for example linked data) to &ldquo;re-envision, expose and share library data as entities (work, people, places, etc.) and &hellip; <a href="http://blogs.pjjk.net/phil/a-library-shaped-black-hole-in-the-web/">Continue reading <span>A library shaped black hole in the web?</span> <span>&rarr;</span></a>'
layout: post
guid: 'http://blogs.pjjk.net/phil/?p=1554'
permalink: 'http://blogs.pjjk.net/phil/a-library-shaped-black-hole-in-the-web/'
enclosure:
    - "\n\n"
syndication_source:
    - 'Sharing and learning'
syndication_source_uri:
    - 'http://blogs.pjjk.net/phil'
syndication_source_id:
    - 'http://blogs.pjjk.net/phil/feed/'
'rss:comments':
    - 'http://blogs.pjjk.net/phil/a-library-shaped-black-hole-in-the-web/#comments'
'wfw:commentRSS':
    - 'http://blogs.pjjk.net/phil/a-library-shaped-black-hole-in-the-web/feed/'
syndication_feed:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed_id:
    - '2'
syndication_permalink:
    - 'http://blogs.pjjk.net/phil/a-library-shaped-black-hole-in-the-web/'
syndication_item_hash:
    - cda4e380d618de3e5d61b33ae87594bf
    - d7e367adcbb3c428c8b0987ce309ec36
    - bc7f16c342902481e619a6221f46cdc5
    - 514321f431c629c7890296d41c48cae7
    - 514321f431c629c7890296d41c48cae7
    - 822f9308510e14f48f8ba503a8703bb7
    - 822f9308510e14f48f8ba503a8703bb7
    - 613e2dc1a9046e1d9034ce20f6fdab1c
    - 32c21c0bebb36eb9a90f912ce6b8f14d
    - 32c21c0bebb36eb9a90f912ce6b8f14d
categories:
    - cetis
    - libraries
    - 'semantic technologies'
---

[A library shaped black hole in the web?](https://www.oclc.org/en-UK/events/2015/Library-shaped-black-hole-161015.html) was the name of an OCLC event that was getting its second(?) run in Edinburgh last week, looking at how libraries can contribute to the web, using new technologies (for example linked data) to “re-envision, expose and share library data as entities (work, people, places, etc.) and what this means.”

Aside: to suggest that libraries act as a *black* hole in the web is quite a strong statement, you see black holes [suck in information](https://en.wikipedia.org/wiki/Black_hole_information_paradox) and at the very least mangle it, if not destroy it completely. Perhaps only a former physicist would read the title that way ![:-)](http://blogs.pjjk.net/phil/wp-includes/images/smilies/simple-smile.png)

We were promised that we would:

> learn how entity-based descriptions of library data – powered by linked data – will create new approaches to cataloguing, resource sharing and discovery. We will look at how referencing library data as entities, in Web friendly formats, enables data relationships to be rendered useful in many more contexts increasing the relevance of libraries within the wider information ecosystem.

which I wouldn’t quibble with. Here’s a summary of what I did take from the day.

[Owen Stephens](http://www.meanboyfriend.com/overdue_ideas/about/) got us started with an introduction to the basic RDF model of triples building in to a graph, pointing out that the basic services required to start doing this are not already available to libraries. So if the statement you wish to make is about the authorship of a book, you need URIs to identify the book, the person and the “has creator” relationship: these first two of these are provided by, for example, the [Library of Congress Authorities](http://authorities.loc.gov/) [linked data service](http://id.loc.gov/), the third by Dublin Core (among others). But Owen stressed that the linked data approach was more than another view of the same data because *other people can make statements about your data*. Owen drew on the distinction made in the Semantic Web community between “open world” and “closed world” approaches to illustrate how this can change your view of data. The library-catalogue-as-inventory is treated “closed world”, that is that all the relevant information could be assumed to be there, so if you don’t have information about a book in your inventory then you infer that you don’t have the book. In an open world, however, someone else might have information that would change that inference, so in an open world approach to using data you wouldn’t take lack of information about something to mean that the thing in question did not exist. The advantage of working in an open world is that further information is always being added by others from other fields, so the catalogue-as-information-source can be just one source of data for a web that goes beyond bibliographic data. Owen gave an example of this from Early English Books, where data extracted from the colophons about the booksellers who had commissioned the printing of each book had been linked to data from historical research on these book sellers (their locations and dates of operation) which greatly enhances the value of the library catalogue data for researchers into the history of publishing. We’ll come back to this theme of enhancing the value of the library catalogue for others.

[Owen has a more complete summary of his presentation available](http://www.meanboyfriend.com/overdue_ideas/2015/05/what-it-means-to-be-open/).

Neil Jefferies of the Bodleian library built on what Owen had been discussing. He identified the core interest of the library as the *intellectual* content of the books, letting archives and museums deal with the book as an object, and he mentioned the hierarchical nature of intellectual content: data -&gt; facts -&gt; information -&gt; knowledge. He also added that the libraries key strengths of the library are expertise in retention and search, and access to the physical originals. technology thought has shifted what the library may achieve, so that it should be about creating knowledge not just holding data or sharing information. He went on to give more examples of projects showing libraries using linked data to facilitate knowledge creation than I could manage to take notes on, but a among the highlights was: [**LD4L**, Linked data for libraries](https://www.ld4l.org/), a $999k Mellon funded project involving Cornell, Harvard and Standford, which aims to create a “Scholarly Resource Semantic Information Store” which works both within individual institutions and links to other domains. the aim is to build this with OSS, and Neil mentioned the [VIVO platform](http://vivoweb.org/) and [community](https://www.w3.org/community/vivo/) as an example of this. Neil also spoke about the richness required in order to model all the information relevant to knowledge in the library. [**CAMELOT**](http://camelot-dev.bodleian.ox.ac.uk/) is the data model used for knowledge held at the Bodleian, it includes a lot of provenance and contextual modelling: linked data is about assertions and you need context and provenance to be able to judge the truth of these (here’s a consequence of the open world nature of linked data, do you know where your data came from? do you know the assumptions made when creating it?). [BIBFRAME](http://www.loc.gov/bibframe/), or MARC in RDF is not enough, it holds on to the idea of central authority of the catalogue(-as-inventory), and in linked data authority is more diffuse. The data model for LD4L will likely include BIBFRAME, [FaBIO](http://www.essepuntato.it/lode/http://purl.org/spar/fabio), [VIVO-ISF](https://wiki.duraspace.org/display/VIVO/VIVO-ISF+Ontology), [OpenAnnotation](http://www.openannotation.org/), [PAV](https://code.google.com/p/pav-ontology/), [OAI-ORE](https://www.openarchives.org/ore/), [SKOS](http://www.w3.org/2004/02/skos/), [VIAF](https://viaf.org/), [ORCHID](http://orcid.org/), [ISNI](http://www.isni.org/), [OCLC Works](https://www.oclc.org/developer/develop/linked-data.en.html), circulation, citation and usage data, and will likely need a deal of entity reconciliation to deal with many people talking about the same thing.

So much for the idea and the promise of linked data for libraries. I would next like to describe a trio of talks that dealt with the question “what is to be done?”

Cathy Dolbear from Oxford University Press spoke about providing semantic and bibliographic data for libraries. The OUP provide metadata in a lot of different ways, varying from the venerable OAI-PMH (which seems to have little uptake) to RDFa embedded in product web pages (which may soon become JSON-LD). And yet most people find OUP content via direct links and search engines, a spot sample of one day’s referrers showed library discovery services accounted for ~1% of the hits. Cathy stressed that there were patches where library discovery services were more significant, but on the whole it was hard to see library use. Internally OUP have their own schema, OxMetaML, and are moving to a more graph-based approach; the transform this to the standard used by discovery services, e.g. [HighWire](http://home.highwire.org/), [PRISM](http://www.idealliance.org/specifications/prism-metadata-initiative), [JATS](http://jats.niso.org/), PubMED etc. Cathy seemed to want to find ways that OUP metadata could be used to support the endeavours of libraries to use linked data as described above, but wanted to know that if she published Linked Data how would it be used–OUP can only spend money on doing things they know people are going to use, but it is hard to see who is using linked data. I got the strong impression that Cathy knew the ideas, and was aware of the project work being done with linked data, but her key point was that OUP need more info from libraries about what data is needed for real-world service delivery before they can be sure whether it’s worth creating &amp; delivering metadata.

[Ken Chad](http://www.kenchadconsulting.com/) spoke about [Linked data why care and what do we do](http://www.kenchadconsulting.com/wp-content/uploads/2015/10/Linked_Data_JTBD_OCLC_Event_Oct2015.pdf) describing the current status of linked data in terms of [chasms in the technology adoption lifecycle](http://chasminstitute.com/) and [troughs of disillusionment in the hype cycle](http://www.gartner.com/technology/research/methodologies/hype-cycle.jsp), both of which echo Cathy’s question about how do we get beyond interesting projects and to real world service delivery. In my own mind this is key. The [initial draft of RDF](http://www.w3.org/TR/WD-rdf-syntax-971002/) is about 18 years old. The [“linked data” reboot](http://www.w3.org/DesignIssues/LinkedData.html) is about 9 years old. When do we stop talking about early adopters and decide we’ve got all the adopters we’re going to get? Or at least if we want more adopters we need a radically different approach. Ken spoke about approaching the problem in terms of the [Jobs to be Done](http://jobstobedone.org/)–the link to Ken’s presentation above describes that approach–which I have no problem with, and I certainly would agree with Ken’s suggestion that the job to be done is to “d<span style="font-weight: 400;">esign a library website that helps students focus less on finding and more on studying”. However,</span> I do think there is an extra layer to this problem in that it requires other people to provide things you can link to. Buying a phone won’t help get a job done if you’re the only person with a phone.

Gill Hamilton of the National Library of Scotland to the theme of how to be ready for linked data even if you’re not convinced. This appealed to me. She gave three top tips: (1) following google, think of [things not strings](https://googleblog.blogspot.co.uk/2012/05/introducing-knowledge-graph-things-not.html) and record URIs not names; (2) you probably need a rich and detailed schema for your own specialised uses of the data, don’t dumb this down to a generic ontology but publish it and map to the generic; (3) concentrate on what you have that’s unique and let other people handle the generic. To these Gill added three lesser tips: license your metadata as CC0, demand better systems and use open vocabularies.

[Richard Wallis](http://dataliberate.com/richardwallis/) gave the final presentation ” the web of data is our oyster” which he stated by describing a view of the development of the web from a web of documents to a web of dynamic documents, to a web of information discovery to a web of data to a web of knowledge (with knowledge graphs and data mining). He suggested that libraries were engaged at the start, but became disengage, maybe even hostile, at the point of the the web of discovery. One change that libraries had missed through this was the move from records (by definition, relating to the past) to living descriptions in terms of entities and relationships. This he suggested had meant that many library projects on sharing data had lead to “linked data silos” which search engines cannot get into. The current approach to giving search engines access to entity and relationship data is schema.org, and Richard described his own work on [extending schema for bibliographic data](https://www.w3.org/community/schemabibex/). Echoing Gill’s second tip he stressed that this was not intended to be an appropriate way to meet the libraries metadata needs, or even the way that libraries should use the web to share data between themselves, but it is a way that libraries can share their data with the web (of discovery, of data, of knowledge) as whole.

All in all, a good day. Nothing spectacularly new, but useful to see it all lined up and presented so coherently. Many thanks to Owen, Neil, Cathy, Ken, Gill and Richard, and to OCLC for arranging the event.