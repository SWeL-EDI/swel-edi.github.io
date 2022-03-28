---
id: 905
title: 'Constructing More Advanced SPARQL Queries'
date: '2019-04-22T13:45:28+01:00'
author: 'Angus Addlesee'
excerpt: "CONSTRUCT queries, VALUES and more property\_paths.It was (quite rightly) pointed out that I strangely did not cover CONSTRUCT queries in my previous tutorial on Constructing SPARQL Queries. Additionally, I then went on to use CONSTRUCT queries in both ..."
layout: post
guid: 'https://medium.com/p/72d5ade1eedc'
permalink: 'https://medium.com/wallscope/constructing-more-advanced-sparql-queries-72d5ade1eedc?source=rss----d173846af2b9--rdf'
enclosure:
    - "\n\n"
syndication_source:
    - 'Rdf in Wallscope on Medium'
syndication_source_uri:
    - 'https://medium.com/wallscope/tagged/rdf?source=rss----d173846af2b9--rdf'
syndication_source_id:
    - 'https://medium.com/feed/wallscope/tagged/rdf'
syndication_feed:
    - 'https://medium.com/feed/wallscope/tagged/rdf'
syndication_feed_id:
    - '4'
syndication_permalink:
    - 'https://medium.com/wallscope/constructing-more-advanced-sparql-queries-72d5ade1eedc?source=rss----d173846af2b9--rdf'
syndication_item_hash:
    - acd609827a9d626fa80e81de8eb5daa8
    - 38d6135a94d0a076d101dc50dcae949f
    - 38d6135a94d0a076d101dc50dcae949f
    - 38d6135a94d0a076d101dc50dcae949f
    - a55fe62bb4b73354dfce030e6bf27354
categories:
    - data-science
    - knowledge-management
    - 'Linked Data'
    - rdf
    - sparql
---

#### CONSTRUCT queries, VALUES and more property paths.

It was (quite rightly) pointed out that I strangely did not cover CONSTRUCT queries in my previous tutorial on [Constructing SPARQL Queries](https://medium.com/wallscope/constructing-sparql-queries-ca63b8b9ac02). Additionally, I then went on to use CONSTRUCT queries in both my [Transforming Tabular Data into Linked Data](https://medium.com/wallscope/using-ontorefine-to-transform-tabular-data-into-linked-data-7277ec8c2c0f) tutorial and the [Linked Data Reconciliation](https://medium.com/wallscope/linked-data-reconciliation-in-graphdb-cd2796d2870b) article.

So, to finally correct this - I will cover them here!

### Contents

SELECT vs CONSTRUCT  
First Basic Example  
\- VALUES  
\- Alternative Property Paths  
Second Basic Example  
Example From the Reconciliation Article  
Example From the Benchmark (Sneak Preview)

### SELECT vs CONSTRUCT

In my last tutorial, I basically ran through SELECT queries from the most basic to some more complex. So what’s the difference?

With selects we are trying to match patterns in the knowledge graph to return results. With constructs we are specifying and building a new graph to return.

In the two tutorials linked (in the intro) I was constructing graphs from tabular data to then insert into a triplestore. I will discuss sections of these later but you should be able to follow the full queries after going through this tutorial.

We usually use CONSTRUCT queries at [Wallscope](https://medium.com/wallscope) to build a graph for the front-end team. Essentially, we create a portable sub-graph that contains all of the information needed to build a section of an application. Then instead of many select queries to the full database, these queries can be run over the much smaller sub-graph returned by the construct query.

### First Basic Example

For this first example I will be querying my Superhero dataset that you can download [here](https://github.com/wallscope/superhero-rdf).

Each superhero entity in this dataset is connected to their height with the predicate dbo:height as shown here:

<figure>![](https://cdn-images-1.medium.com/max/1024/1*xrVRyz9qsBT6BsUDPPgIAw.png)</figure>Using this basic SELECT query:

```
PREFIX dbo: <<a href="http://dbpedia.org/ontology/">http://dbpedia.org/ontology/</a>>
```

```
SELECT ?hero ?height<br></br>WHERE {<br></br>    ?hero dbo:height ?height .<br></br>}
```

Now lets modify this query slightly into a CONSTRUCT that is almost the same:

```
PREFIX dbo: <<a href="http://dbpedia.org/ontology/">http://dbpedia.org/ontology/</a>>
```

```
CONSTRUCT {<br></br>    ?hero dbo:height ?height<br></br>} WHERE {<br></br>    ?hero dbo:height ?height .<br></br>}
```

As you can see, this returns the same information but in the form: subject, predicate, object.

<figure>![](https://cdn-images-1.medium.com/max/1024/1*xFyDs2Gi6pLGF7VYiGxRBQ.png)</figure>This is obviously trivial and not entirely useful but we can play with this graph in the construct with only one condition:

> All variables in the CONSTRUCT **must** be in the WHERE clause.

Basically, like in a SELECT query, the WHERE clause matches patterns in the knowledge graph and returns any variables. The difference with a CONSTRUCT is that these variables are then used to build the graph described in the CONSTRUCT clause.

Hopefully that is clear, but it makes more sense if we change the graph description.

For example, if we decided that we wanted to use schema instead of DBpedia’s ontology, we could switch to it in the first clause:

```
PREFIX dbo: <<a href="http://dbpedia.org/ontology/">http://dbpedia.org/ontology/</a>><br></br>PREFIX schema: <<a href="http://schema.org/">http://schema.org/</a>>
```

```
CONSTRUCT {<br></br>    ?hero schema:height ?height<br></br>} WHERE {<br></br>    ?hero dbo:height ?height .<br></br>}
```

This then returns the superheroes attached to their heights with the schema:height predicate as the variables are matched in the WHERE clause and then recombined in the CONSTRUCT clause.

<figure>![](https://cdn-images-1.medium.com/max/1024/1*8ueRPEin_wFtQa0PzdGGAQ.png)</figure>This simple predicate switching is not entirely useful on it’s own (unless you really need to switch ontology for some reason) but is a good first step to understand this type of query.

To create some more useful CONSTRUCT queries, I’ll first go through VALUES and another type of property path.

### VALUES

I’m sure there are many use-cases in which the VALUES clause is incredibly useful but I can’t say that I use it often. Essentially, it allows data to be provided within the query.

If you are searching for a particular sport in a dataset for example, you could match all entities that are sports and then filter the results for it. This gets more complex however if you are looking for a few particular sports and you may want to provide the few sports within the query.

With VALUES you can constrain your query by creating a variable (can also create multiple variables) and assigning it some data.

I tend to use this with federated queries to grab data (usually for insertion into my database) about a few particular entities.

Let’s go through a practical example of this:

```
PREFIX dbr: <<a href="http://dbpedia.org/resource/">http://dbpedia.org/resource/</a>>
```

```
SELECT ?country ?pop<br></br>WHERE {<br></br>    VALUES ?country {<br></br>        dbr:Scotland<br></br>        dbr:England<br></br>        dbr:Wales<br></br>        dbr:Northern_Ireland<br></br>        dbr:Ireland<br></br>    }<br></br>}
```

In this example I am interested in the five largest countries in the British Isles to compare populations. For reference (I’m from Scotland and had to check I was correct so imagine others may find this useful also):

<figure>![](https://cdn-images-1.medium.com/max/474/0*KpQtDlqz1iyxh-av)<figcaption>[source](https://www.ordnancesurvey.co.uk/blog/2011/08/whats-the-difference-between-uk-britain-and-british-isles/)</figcaption></figure>I am using DBpedia for this example so I have assigned the five country entities to the variable ?countries and selected them to be returned.

<figure>![](https://cdn-images-1.medium.com/max/1024/1*YnhPgk507n11ojV-RlF-1A.png)</figure>It should therefore be easy enough to grab the corresponding populations you’d think. I add the SERVICE clause to make this a federated query ([covered previously](https://medium.com/wallscope/constructing-sparql-queries-ca63b8b9ac02)). This just sends the countries defined within the query to DBpedia and returns their corresponding populations.

```
PREFIX dbr: <<a href="http://dbpedia.org/resource/">http://dbpedia.org/resource/</a>><br></br>PREFIX dbp: <<a href="http://dbpedia.org/property/">http://dbpedia.org/property/</a>>
```

```
SELECT ?country ?pop<br></br>WHERE {<br></br>    VALUES ?country {<br></br>        dbr:Scotland<br></br>        dbr:England<br></br>        dbr:Wales<br></br>        dbr:Northern_Ireland<br></br>        dbr:Ireland<br></br>    }<br></br><br></br>    SERVICE <<a href="http://dbpedia.org/sparql">http://dbpedia.org/sparql</a>> {<br></br>        ?country dbp:populationCensus ?pop .<br></br>    }<br></br>}
```

Here are the results:

<figure>![](https://cdn-images-1.medium.com/max/1024/1*i4Ch5_xNk-n9L7J5XsnUEA.png)</figure>You will notice however that Ireland is missing from the results! You will often find this kind of problem with linked open data, the structure is not always consistent throughout.

To find Ireland’s population we need to switch the predicate from dbp:populationCensus to dbo:populationTotal like so:

```
PREFIX dbr: <<a href="http://dbpedia.org/resource/">http://dbpedia.org/resource/</a>><br></br>PREFIX dbo: <<a href="http://dbpedia.org/ontology/">http://dbpedia.org/ontology/</a>>
```

```
SELECT ?country ?pop<br></br>WHERE {<br></br>    VALUES ?country {<br></br>        dbr:Scotland<br></br>        dbr:England<br></br>        dbr:Wales<br></br>        dbr:Northern_Ireland<br></br>        dbr:Ireland<br></br>    }<br></br><br></br>    SERVICE <<a href="http://dbpedia.org/sparql">http://dbpedia.org/sparql</a>> {<br></br>        ?country dbo:populationTotal ?pop .<br></br>    }<br></br>}
```

which returns Ireland alongside its population… but none of the others:

<figure>![](https://cdn-images-1.medium.com/max/1024/1*0ubSgXQgSQRG74xdTuCthA.png)</figure>This is of course a problem but before we can construct a solution, let’s run through alternate property paths.

### Alternative Property Paths

In [my last SPARQL tutorial](https://medium.com/wallscope/constructing-sparql-queries-ca63b8b9ac02) we covered sequential property paths which (once the [benchmark](https://medium.com/wallscope/comparison-of-linked-data-triplestores-developing-the-methodology-e87771cb3011?source=friends_link&sk=69ab0d1ab9cc91554967332fa1a2ca2c) query templates come out) you may notice I am a big fan of.

Another type of property path that I use fairly often is called the Alternative Property Path and is made use of with the pipe (|) character.

If we look back at the problem above in the VALUES section, we can get some populations with one predicate and the rest with another. The alternate property path allows us to match patterns with **either**! For example, if we modify the population query above we get:

```
PREFIX dbr: <<a href="http://dbpedia.org/resource/">http://dbpedia.org/resource/</a>><br></br>PREFIX dbp: <<a href="http://dbpedia.org/property/">http://dbpedia.org/property/</a>><br></br>PREFIX dbo: <<a href="http://dbpedia.org/ontology/">http://dbpedia.org/ontology/</a>>
```

```
SELECT ?country ?pop<br></br>WHERE {<br></br>    VALUES ?country {<br></br>        dbr:Scotland<br></br>        dbr:England<br></br>        dbr:Wales<br></br>        dbr:Northern_Ireland<br></br>        dbr:Ireland<br></br>    }<br></br><br></br>    SERVICE <<a href="http://dbpedia.org/sparql">http://dbpedia.org/sparql</a>> {<br></br>        ?country dbp:populationCensus | dbo:populationTotal ?pop .<br></br>    }<br></br>}
```

This is such a simple change but so powerful as we now return every country alongside their population with one relatively basic query:

<figure>![](https://cdn-images-1.medium.com/max/1024/1*dUIFD19xhY2Pb56wdVr5uQ.png)</figure>This SELECT is great if we are just looking to find some results but what if we want to store this data in our knowledge graph?

### Second Example

It would be a hassle to have to use this alternative property path every time we want to work with country populations. In addition, if users were not aware of this inconsistency, they could find and report incorrect results.

This is why we CONSTRUCT the result graph we want without the inconsistencies. In this case I have chosen dbo:populationTotal as I simply prefer it and use that to connect countries and their populations:

```
PREFIX dbr: <<a href="http://dbpedia.org/resource/">http://dbpedia.org/resource/</a>><br></br>PREFIX dbp: <<a href="http://dbpedia.org/property/">http://dbpedia.org/property/</a>><br></br>PREFIX dbo: <<a href="http://dbpedia.org/ontology/">http://dbpedia.org/ontology/</a>>
```

```
CONSTRUCT {<br></br>    ?country dbo:populationTotal ?pop<br></br>} WHERE {<br></br>    VALUES ?country {<br></br>        dbr:Scotland<br></br>        dbr:England<br></br>        dbr:Wales<br></br>        dbr:Northern_Ireland<br></br>        dbr:Ireland<br></br>    }<br></br><br></br>    SERVICE <<a href="http://dbpedia.org/sparql">http://dbpedia.org/sparql</a>> {<br></br>        ?country dbp:populationCensus | dbo:populationTotal ?pop .<br></br>    }<br></br>}
```

This query returns the countries and their populations like we saw in the previous section but then connects each country to their population with dbo:populationTotal as described in the CONSTRUCT clause. This returns consistent triples:

<figure>![](https://cdn-images-1.medium.com/max/1024/1*KVQHrTVRoaC8yTkIc22DGQ.png)</figure>This is useful if we wish to store this data as the fact it’s consistent will help avoid the problems mentioned above. I used this technique in one of my previous articles so lets take a look.

### Example From Reconciliation Tutorial

This example is copied directly from my data reconciliation tutorial [here](https://medium.com/wallscope/linked-data-reconciliation-in-graphdb-cd2796d2870b). In that article I discuss this query in a lot more detail.

In brief, what I was doing here was grabbing car manufacturer names from tabular data and enhancing that information to store and analyse.

```
PREFIX rdf: <<a href="http://www.w3.org/1999/02/22-rdf-syntax-ns#">http://www.w3.org/1999/02/22-rdf-syntax-ns#</a>><br></br>PREFIX rdfs: <<a href="http://www.w3.org/2000/01/rdf-schema#">http://www.w3.org/2000/01/rdf-schema#</a>><br></br>PREFIX dbo: <<a href="http://dbpedia.org/ontology/">http://dbpedia.org/ontology/</a>><br></br>PREFIX dbp: <<a href="http://dbpedia.org/property/">http://dbpedia.org/property/</a>>
```

```
CONSTRUCT {<br></br>  ?car rdfs:label ?taggedname ;<br></br>       rdf:type dbo:Company ;<br></br>       dbo:location ?location .<br></br><br></br>  ?location rdf:type dbo:Country ;<br></br>            rdfs:label ?lname ;<br></br>            dbp:populationCensus ?pop .<br></br>} WHERE {<br></br>  ?c <urn:col:carNames> ?cname .<br></br><br></br>  BIND(STRLANG(?cname, "en") AS ?taggedname)<br></br><br></br>  SERVICE <<a href="https://dbpedia.org/sparql">https://dbpedia.org/sparql</a>> {<br></br><br></br>    ?car rdfs:label ?taggedname ;<br></br>         dbo:location | dbo:locationCountry ?location .<br></br><br></br>    ?location rdf:type dbo:Country ;<br></br>              rdfs:label ?lname ;<br></br>              dbp:populationCensus | dbo:populationTotal ?pop .<br></br><br></br>    FILTER (LANG(?lname) = "en")<br></br>  }<br></br>}
```

There is little point repeating myself here so if interested, please [take a look](https://medium.com/wallscope/linked-data-reconciliation-in-graphdb-cd2796d2870b?source=friends_link&sk=0edbd82416d6ad46e890a359b7421a4b). What I am trying to display here is that I have used both the alternative property path (twice!) and the CONSTRUCT clause previously in an example use-case.

> Construct queries are perfectly suited to ensuring any data you store is well typed, structured and **importantly** consistent.

I have been short on time since starting my [new project](https://companyconnecting.com/news/conversational-ai-angus-addlesee-heriot-watt) but I am still working on the [benchmark](https://medium.com/wallscope/comparison-of-linked-data-triplestores-developing-the-methodology-e87771cb3011?source=friends_link&sk=69ab0d1ab9cc91554967332fa1a2ca2c) in development.

### Example From The Benchmark (Sneak Preview)

The benchmark repository is not yet public as I don’t want opinions to be formed before it is fleshed out a little more.

I thought it would be good however to give a real (not made for a tutorial) example query that uses what this article teaches:

```
PREFIX dbo: <<a href="http://dbpedia.org/ontology/">http://dbpedia.org/ontology/</a>><br></br>PREFIX schema: <<a href="http://schema.org/">http://schema.org/</a>><br></br>PREFIX dbp: <<a href="http://dbpedia.org/property/">http://dbpedia.org/property/</a>><br></br>INSERT {<br></br>    ?city dbo:populationTotal ?pop<br></br>} WHERE {    <br></br>    {<br></br>      SELECT ?city (MAX(?apop) AS ?pop) {<br></br>          ?user schema:location ?city .<br></br><br></br>          SERVICE <<a href="https://dbpedia.org/sparql">https://dbpedia.org/sparql</a>> {<br></br>            ?city dbo:populationTotal | dbp:populationCensus ?apop .<br></br>          }<br></br>      }<br></br>      GROUP BY ?city<br></br>    }<br></br>}
```

You will notice that this does not contain the CONSTRUCT clause but INSERT instead. You will see me do this switch in both the articles I linked in the introduction. Basically this does nothing too different, the graph that is constructed is inserted into your knowledge graph instead of just returned. The same can be done with the DELETE clause to remove patterns from your knowledge graph.

This query is very similar to the examples throughout this article (by design of course) but grabs countries populations from DBpedia and inserts them into the graph. This is just one point within the query cycle at which the graph changes structure in the benchmark.

Finally, the MAX population is grabbed because some countries in DBpedia have two different populations attached to them…

### Conclusion

Hopefully this is useful for some of you! We have covered why and how to use construct queries along with values and alternative property paths.

At the end of May I am going to the [DBpedia community meeting in Leipzig](https://wiki.dbpedia.org/meetings/Leipzig2019) so my next linked data article will likely cover things I learned at that event or progress on the benchmark development.

In the meantime I will be releasing my next Computer Vision article and another dive into natural conversation.

![](https://medium.com/_/stat?event=post.clientViewed&referrerSource=full_rss&postId=72d5ade1eedc)- - - - - -

[Constructing More Advanced SPARQL Queries](https://medium.com/wallscope/constructing-more-advanced-sparql-queries-72d5ade1eedc) was originally published in [Wallscope](https://medium.com/wallscope) on Medium, where people are continuing the conversation by highlighting and responding to this story.