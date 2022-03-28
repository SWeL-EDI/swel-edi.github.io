---
id: 339
title: 'LRMI balloon debate at #DCMI16 Metadata Summit, Copenhagen'
date: '2016-10-27T14:25:56+01:00'
author: 'Phil Barker'
excerpt: 'I&nbsp;summarised the&nbsp;presentations given at the LRMI workshop &ldquo;Building on Schema.org to describe learning resources&rdquo;&nbsp;at the Dublin Core conference in my previous post,&nbsp;this post is about the discussion part of the workshop. The discussion was organised along the lines of a balloon debate: A balloon debate is a debate in which a number of speakers attempt &hellip; <a href="http://blogs.pjjk.net/phil/lrmi-balloon-debate-at-dcmi16-metadata-summit-copenhagen/">Continue reading <span>LRMI balloon debate at #DCMI16 Metadata Summit, Copenhagen</span> <span>&rarr;</span></a>'
layout: post
guid: 'http://blogs.pjjk.net/phil/?p=1633'
permalink: 'http://blogs.pjjk.net/phil/lrmi-balloon-debate-at-dcmi16-metadata-summit-copenhagen/'
enclosure:
    - "\n\n"
syndication_source:
    - 'Sharing and learning'
syndication_source_uri:
    - 'http://blogs.pjjk.net/phil'
syndication_source_id:
    - 'http://blogs.pjjk.net/phil/feed/'
'rss:comments':
    - 'http://blogs.pjjk.net/phil/lrmi-balloon-debate-at-dcmi16-metadata-summit-copenhagen/#respond'
'wfw:commentRSS':
    - 'http://blogs.pjjk.net/phil/lrmi-balloon-debate-at-dcmi16-metadata-summit-copenhagen/feed/'
syndication_feed:
    - 'http://blogs.pjjk.net/phil/feed/'
syndication_feed_id:
    - '2'
syndication_permalink:
    - 'http://blogs.pjjk.net/phil/lrmi-balloon-debate-at-dcmi16-metadata-summit-copenhagen/'
syndication_item_hash:
    - 264d8c5f5e2bc0f146218581860747cc
    - a84f3ff2b66948b331b8b1e18ee77b88
    - a84f3ff2b66948b331b8b1e18ee77b88
    - 5b3b12bcbb8743b082faed6f93a8748a
    - c561dfd7cff49d0b5bb091caa1b164de
    - 5c6c395fb6abb3e7b34227b407576cf2
categories:
    - DublinCore
    - LRMI
    - metadata
---

I [summarised the presentations](http://blogs.pjjk.net/phil/lrmi-at-dcmi16-metadata-summit-copenhagen/) given at the LRMI workshop “[Building on Schema.org to describe learning resources](http://dcevents.dublincore.org/IntConf/index/pages/view/specSession#lrmi)” at the Dublin Core conference in my previous post, this post is about the discussion part of the workshop. The discussion was organised along the lines of a balloon debate:

> A balloon debate is a debate in which a number of speakers attempt to win the approval of an audience. The audience is invited to imagine that the speakers are flying in a hot-air balloon which is sinking and that someone must be thrown out if everyone is not to die. Each speaker has to make the case why they should not be thrown out of the balloon to save the remainder.

[https://en.wikipedia.org/wiki/Balloon\_debate](https://en.wikipedia.org/wiki/Balloon_debate)

Our “balloon” is a metaphorical one, it stands for the volunteer effort that maintains LRMI (LRMI seeming somewhat like a balloon in that it is kept going by hot air), and instead of carrying people it is trying to carry out work that will help people describe learning resources. While it is by no means sinking, like a real balloon LRMI can only sustain a certain (work-)load, and so we need to be selective in the work which is taken on. This exercise was intended to provide LRMI with ideas about which work to prioritize, while providing those who take part with information about the future directions that are open to LRMI.

### Debate format

The debate proceeded through three rounds, the first round was about choosing candidate ideas for future work, the second eliminated those which seemed least feasible, and the third was to select the highest priority ideas. On the day we didn’t really get to the third round, but the results were nonetheless interesting.

### The Ideas

We started with the following ideas, seeded by myself with help from other members of the LRMI task group (especially Stuart Sutton who provided several of the descriptions).

<dl><dt>1. Structured, controlled vocabularies for LRMI properties.</dt><dd>Several key LRMI properties take text for their expected value type. The use of free text for properties such as learningResourceType makes it difficult to compare data from different providers. Where there are suggested values mentioned in the LRMI spec for these, the LRMI Task Group is already working to provide definitions of terms in RDF (as SKOS Concepts). This suggestion is a continuation of this work, to try as far as possible to provide controlled vocabularies for relevant LRMI properties.</dd><dt>2. Drop the Alignment Object for the most common alignment types</dt><dd>The mechanism of indicating how a resource relates to an educational framework involves a level of indirection which is both arcane and potentially powerful, however it’s full power is not fully developed. The suggestion here is that the indirection be removed by creating properties for those alignment types which are clearly important. So, for example, it is often important to state the educational level of a resource (e.g. in terms of Grade Level). Currently this would be an educationalAlignment with an AlignmentObject having alignmentType of educationalLevel. The indirection of the AlignmentObject could be removed if there were a property of a learning resource called educationalLevel referencing directly a point in a grade level framework. [![Figure 1a: representing an educational alignment with an alignment object. The alignment type property of the alignment object can set to specify the nature of the relationship, e.g. that this represents the educational level of the resource.](http://blogs.pjjk.net/phil/content/uploads/educationalAlignment-simpleSchemaGraph-1-640x323.png)](http://blogs.pjjk.net/phil/content/uploads/educationalAlignment-simpleSchemaGraph-1.png)***Figure 1a:*** representing an educational alignment with an alignment object.  
The alignment type property of the alignment object can set to specify the nature of the relationship, e.g. that this represents the educational level of the resource.

***[![simplifiedalignment-simpleschemagraph](http://blogs.pjjk.net/phil/content/uploads/simplifiedAlignment-simpleSchemaGraph-1.png)](http://blogs.pjjk.net/phil/content/uploads/simplifiedAlignment-simpleSchemaGraph-1.png)Figure 1b:*** a possible way of representing an alignment such as educational level of the resource more simply. Note: the value provided could be text or a URI; representing the relationship of the node to an educational framework is not yet solved in Schema.org.

</dd><dt>3. Develop the Alignment Object to be more expressive</dt><dd>The mechanism of indicating how a resource relates to an educational framework involves a level of indirection which is both arcane and potentially powerful, however it’s full power is not fully developed. The suggestion here is that properties be added to the AlignmentObject to allow additional information about the alignment between a resource and a point in an educational framework. This additional information may include factors such as: who asserts that the alignment holds, what evidence they have for this alignment, how good is the alignment.</dd><dt>4. Recommendations for referring to educational frameworks</dt><dd>From the point of view of facilitating resource discovery the relationship between a resource and an educational framework is key. Showing how a resource relates to a framework which is understood by educators and learners allows them to find resource suitable for their needs. This may be manifest in discovery interfaces as faceted search or browse categories. One problem is identifying the relevant frameworks for different types of educational alignment in different educational contexts (e.g. what is the Scottish equivalent of K-12 for educational level?). Another problem is that variation in how these frameworks are expressed in LRMI metadata makes creation of such services more difficult than it need be (what is the framework name for K-12? What URIs are best to use?). We could help by creating an inventory of frequently used educational frameworks and recommendations on how to refer to them.</dd><dt>5. Declare a “Learning Resource” type</dt><dd>Currently, a Learning Resource is not formally declared in the schema.org schema as a subtype of CreativeWork. Instead, it is inferred that a Learning Resource is a kind of CreativeWork since the LRMI properties were included as part of the CreativeWork type. The lack of an explicit LearningResource subtype to CreativeWork makes it difficult for some doing markup or implementing systems using schema.org to recognize that schema.org in fact supports description of learning resources. They see EducationEvent as a subtype of Event, but no LearningResource as a subtype of CreativeWork.</dd><dt>6. Define a minimal subset of schema.org for describing learning materials</dt><dd>The schema.org schema is quite large and can be intimidating for some wanting to define minimally viable learning resource descriptions–e.g., where to begin, what properties are most important, how should they be used. Publishing a suggested profile of schema.org that defines a minimaly viable learning resource description while leaving open the addition of other properties needed with a particular use, might assist implementers needing a means to jumpstart development of their own profile based in schema.org.</dd><dt>7. Create support materials explaining LRMI properties</dt><dd>Recently, examples of how to use the AlignmentObject as well as the LRMI properties of CreativeWork have been added as ‘footers’ to the relevant schema pages at schema.org. While an excellent beginning, these additions are not enough. Other types of support materials for describing learning resources using the LRMI properties and classes need to be defined, developed, and published. Such materials might include a one-stop “primer” that combines narrative with examples and covers the inevitable points in usage where subjective decisions must be made where there are alternative legitimate paths forward.</dd><dt>8. Collate information about existing LRMI implementations</dt><dd>Specifications always need to be interpreted in order to be used in specific contexts, and however much normative and informative material is provided, we cannot hope to cover all contexts. One way that people implementing a specification can make choices that do not lead to unnecessary divergence is by referring to other implementations from similar contexts. LRMI could facilitate this by collating information about where these implementations can be found. This may also be useful in monitoring the uptake of the specification, identifying problems commonly encountered and providing examples of good practice.</dd><dt>9. Create an editor for LRMI metadata</dt><dd>Several tools exist that can create LRMI metadata within the scope of a single project or service’s needs. What is suggested here is that LRMI create, assist or promote the creation of an editor that can serve as a reference implementation: independent of the choices that would need to be made for any use in practice but flexible enough to be tailored practical use and, importantly, illustrating good practice in the implementation of LRMI.</dd><dd></dd></dl>## The voting

[![voting from LRMI workshop DCMI Copenhage](http://blogs.pjjk.net/phil/content/uploads/2016-10-13-17.01.01-270x480.jpg)](http://blogs.pjjk.net/phil/content/uploads/2016-10-13-17.01.01.jpg)In the end we discussed and voted on the issues of which ideas seemed most appealing and then, after eliminating those ideas which were not popular, we discussed and voted on the ideas that seemed least feasible, then had a short discussion about the results. We kept a tally of the votes on a flip chart: green ticks for ideas we thought attractive, red ticks for those we thought least feasible.

The ideas most liked were:

- Structured, controlled vocabularies for LRMI properties,
- Define a minimal subset of schema.org for describing learning materials, and
- Collate information about existing LRMI implementations.

As was pointed out in the discussion, there are relationships between the ideas which mean that some other ideas become easier if these are achieved first (e.g. a general purpose editor becomes easier if you have agreed a general purpose subset of schema for it to edit).

Those ideas which we thought most difficult to achieve were

- Structured, controlled vocabularies for LRMI properties and
- Declare a “Learning Resource” type.

The specific issues with both of these centred around achieving agreement or consensus on terms and definitions.

I’m pretty sure that everyone involved in LRMI will see something in these results that they think a sensible outcome and something which raises an eyebrow or two. I’m also fairly sure that it won’t be the same things for everyone.. which is to say, the discussions will continue.

## So what now?

Some of the ideas discussed are based on work that individuals or groups involved in LRMI are already scoping out. As a group we have made a start on formally describing some values for use with LRMI terms as SKOS concepts (see the [DCMI/LRMI Github repository](https://github.com/dcmi/LRMI_Vocabs)). I have had a masters student work on creating a subset of schema.org for learning resources. There is an editor for LRMI in the works, which looks like it could meet the sort of requirements described above. And as I described in the [presentation](https://docs.google.com/presentation/d/1SnFKo-wUs4BUPoR2H-LUIxVNLSl8WNFj2KbmrFSBzxQ/edit?usp=sharing) I gave at the workshop, there is work describing how LRMI is used. So hopefully we will be able to make progress on some of these ideas.

As I said during the workshop, LRMI is a volunteer effort. People work on whichever aspects of it interests them. If you are interested in any of the ideas described above, or have some other ideas that you think would be valuable, please join us and I hope will be able to achieve more together.