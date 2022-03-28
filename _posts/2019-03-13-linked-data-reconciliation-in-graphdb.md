---
id: 849
title: 'Linked Data Reconciliation in GraphDB'
date: '2019-03-13T10:15:50+00:00'
author: 'Angus Addlesee'
excerpt: "Using DBpedia to Enhance your Data in\_GraphDBFollowing my article on Transforming Tabular Data into Linked Data using OntoRefine in GraphDB, the founder of Ontotext (Atanas Kiryakov) suggested I write a further tutorial using GraphDB for data reconcili..."
layout: post
guid: 'https://medium.com/p/cd2796d2870b'
permalink: 'https://medium.com/wallscope/linked-data-reconciliation-in-graphdb-cd2796d2870b?source=rss----d173846af2b9--rdf'
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
    - 'https://medium.com/wallscope/linked-data-reconciliation-in-graphdb-cd2796d2870b?source=rss----d173846af2b9--rdf'
syndication_item_hash:
    - 24e038aa6763c233d804699863c00db4
    - 6b8d504933b7dfdad1b6f0b922a9b990
    - 618bfdcf26081ff19187edcbbc183c9f
    - 618bfdcf26081ff19187edcbbc183c9f
    - 618bfdcf26081ff19187edcbbc183c9f
    - 46484523b3698a234c36f70e7c293492
categories:
    - database
    - dbpedia
    - graphdb
    - 'Linked Data'
    - rdf
---

#### Using DBpedia to Enhance your Data in GraphDB

Following my article on [Transforming Tabular Data into Linked Data using OntoRefine in GraphDB](https://medium.com/wallscope/using-ontorefine-to-transform-tabular-data-into-linked-data-7277ec8c2c0f), the founder of Ontotext ([Atanas Kiryakov](https://twitter.com/kiryakov_ak)) suggested I write a further tutorial using GraphDB for data reconciliation.

In this tutorial we will begin with a .csv of car manufacturers and enhance this with DBpedia. This .csv can be downloaded from [here](https://github.com/wallscope/reconciliation) if you want to follow along.

### Contents

**Setting Up  
Constructing the Graph  
Reconciling your Data  
Exploring the New Graph  
Conclusion**

### Setting Up

First things first, we need to load our tabular data into OntoRefine in GraphDB. Head to the import tab, select “Tabular (OntoRefine)” and upload cars.csv if you are following along.

<figure>![](https://cdn-images-1.medium.com/max/1024/1*cGn-wLtyhbax067tgwzDiA.png)</figure>Click “Next” to start creating the project.

<figure>![](https://cdn-images-1.medium.com/max/1024/1*Sm59STd4LZ8qZ9M9Y3Jq9w.png)</figure>On this screen you need to **untick** “Parse next 1 line(s) as column headers” as this .csv does not have a header row. Rename the project in the top right corner and click “Create Project”.

<figure>![](https://cdn-images-1.medium.com/max/1024/1*ZwVZVINqkzfo64OT2GNnAg.png)</figure>You should now have this screen (above) showing one column of car manufacturer names. The column has a space in it which is annoying when running SPARQL queries across so lets rename it.

<figure>![](https://cdn-images-1.medium.com/max/459/1*Qe61NxrbrCxmtegnzHkm8Q.png)</figure>Click the little arrow next to “Column 1”, open “Edit Column” and then click “Rename this Column”. I called it “carNames” and will use this in the queries below so remember if you name it something different.

<figure>![](https://cdn-images-1.medium.com/max/714/1*AfDnzCuxzDodO0et2zbW0Q.png)</figure>If you ever make a mistake, remember there is and undo/redo tab.

### Constructing the Graph

In the top right of the interface there is an orange button titled “SPARQL”. Click this to open the SPARQL interface from which you can query your tabular data.

<figure>![](https://cdn-images-1.medium.com/max/1024/1*sVduinlx5H6DAwNPLiqjRg.png)</figure>In the above screenshot I have run the query we want. I have have pasted it here so you can see it all and I go through it in detail below.

> I use a CONSTRUCT query here. If you are new to SPARQL entirely then I recommend reading my tutorial on [Constructing SPARQL Queries](https://medium.com/wallscope/constructing-sparql-queries-ca63b8b9ac02) first. I then wrote a second tutorial, which covers constructs, called [Constructing More Advanced SPARQL Queries](https://medium.com/wallscope/constructing-more-advanced-sparql-queries-72d5ade1eedc) for those that need.

```
PREFIX rdf: <<a href="http://www.w3.org/1999/02/22-rdf-syntax-ns#">http://www.w3.org/1999/02/22-rdf-syntax-ns#</a>><br></br>PREFIX rdfs: <<a href="http://www.w3.org/2000/01/rdf-schema#">http://www.w3.org/2000/01/rdf-schema#</a>><br></br>PREFIX dbo: <<a href="http://dbpedia.org/ontology/">http://dbpedia.org/ontology/</a>><br></br>PREFIX dbp: <<a href="http://dbpedia.org/property/">http://dbpedia.org/property/</a>>
```

```
CONSTRUCT {<br></br>  ?car rdfs:label ?taggedname ;<br></br>       rdf:type dbo:Company ;<br></br>       dbo:location ?location .<br></br><br></br>  ?location rdf:type dbo:Country ;<br></br>            rdfs:label ?lname ;<br></br>            dbp:populationCensus ?pop .<br></br>} WHERE {<br></br>  ?c <urn:col:carNames> ?cname .<br></br><br></br>  BIND(STRLANG(?cname, "en") AS ?taggedname)<br></br><br></br>  SERVICE <<a href="https://dbpedia.org/sparql">https://dbpedia.org/sparql</a>> {<br></br><br></br>    ?car rdfs:label ?taggedname ;<br></br>         dbo:location | dbo:locationCountry ?location .<br></br><br></br>    ?location rdf:type dbo:Country ;<br></br>              rdfs:label ?lname ;<br></br>              dbp:populationCensus | dbo:populationTotal ?pop .<br></br><br></br>    FILTER (LANG(?lname) = "en")<br></br>  }<br></br>}
```

I start this query by defining my prefixes as usual. I am wanting to construct a graph around these car manufacturers so I design that in my CONSTRUCT clause. I am building a fairly simple graph for this tutorial so lets just run through it very quickly.

I want to have entities representing car manufacturers that have a type, label and location. This location is the headquarters of the car manufacturer. In most cases, all entities should have both a type and a human-readable label so I have ensured this here.

Each location is also an entity with an attached type, label and population.

Unlike my [superhero tutorial](https://medium.com/wallscope/using-ontorefine-to-transform-tabular-data-into-linked-data-7277ec8c2c0f), the .csv only contains the car company names and not all the data we want in our graph. We therefore need to reconcile our data with information in an open linked dataset. In this tutorial we will use DBpedia, the linked data representation of Wikipedia.

To get the information needed to build the graph declared in our CONSTRUCT we first grab all the names in our .csv and assign them to the variable ?cname. String literals must be language tagged to reconcile with the data in DBpedia so I BIND the English language tag “en” to each string literal. This explanation is what the lines below do:

> If you didn’t name the column “carNames” above, you will have to modify the &lt;urn:col:carNames&gt; predicate here.

```
  ?c <urn:col:carNames> ?cname .<br></br><br></br>  BIND(STRLANG(?cname, "en") AS ?taggedname)
```

Following this we use the SERVICE tag to send the query to DBpedia (this is called a federated query). We find every entity with the label matching our language tagged strings from the original .csv.

Once I have those entities, I need to find their locations. DBpedia is a very messy dataset so we have to use an alternative path in the query (represented by the “pipe” | symbol). This finds locations connected by any of the alternate paths given (in this case dbo:location and dbo:locationCountry) and assigns them to the variable ?location.

That explanation is referring to these lines:

```
    ?car rdfs:label ?taggedname ;<br></br>         dbo:location | dbo:locationCountry ?location .
```

Next we want to retrieve the information about each country. The first pattern in the location ensures the entity has the type dbo:Country so that we don’t find loads of irrelevant locations.

Following this we grab the label and again use alternate property paths to extract each countries population.

> It is important to note that some countries have two different populations attached by these two predicates.

We finally FILTER the country labels to only return those that are in English as that is the language our original dataset is in. Data reconciliation can also be used to extend your data into other languages if it happens to fit a multilingual linked open dataset.

That covers the final few lines of our query:

```
    ?location rdf:type dbo:Country ;<br></br>              rdfs:label ?lname ;<br></br>              dbp:populationCensus | dbo:populationTotal ?pop .<br></br><br></br>    FILTER (LANG(?lname) = "en")
```

Next we need to insert this graph we have constructed into a GraphDB repository.

<figure>![](https://cdn-images-1.medium.com/max/674/1*jy505iGtKh8vLAep8Y_WVQ.png)</figure>Click “SPARQL endpoint” and copy your endpoint (will be different) to be used later.

### Reconciling the Data

If you have not done already, create a repository and head to the SPARQL tab.

> You can see in the top right of this screenshot that I’m using a repository called “cars”.

<figure>![](https://cdn-images-1.medium.com/max/1024/1*u_uHZZJKqxlpbmTs5pKF-w.png)</figure>In this query panel you want to copy the CONSTRUCT query we built and modify it a little. The full query is here:

```
PREFIX rdf: <<a href="http://www.w3.org/1999/02/22-rdf-syntax-ns#">http://www.w3.org/1999/02/22-rdf-syntax-ns#</a>><br></br>PREFIX rdfs: <<a href="http://www.w3.org/2000/01/rdf-schema#">http://www.w3.org/2000/01/rdf-schema#</a>><br></br>PREFIX dbo: <<a href="http://dbpedia.org/ontology/">http://dbpedia.org/ontology/</a>><br></br>PREFIX dbp: <<a href="http://dbpedia.org/property/">http://dbpedia.org/property/</a>>
```

```
INSERT {<br></br>  ?car rdfs:label ?taggedname ;<br></br>       rdf:type dbo:Company ;<br></br>       dbo:location ?location .<br></br><br></br>  ?location rdf:type dbo:Country ;<br></br>            rdfs:label ?lname ;<br></br>            dbp:populationCensus ?pop .<br></br>} WHERE { SERVICE <http://localhost:7200/rdf-bridge/yourID> {<br></br>  ?c <urn:col:carNames> ?cname .<br></br><br></br>  BIND(STRLANG(?cname, "en") AS ?taggedname)<br></br><br></br>  SERVICE <<a href="https://dbpedia.org/sparql">https://dbpedia.org/sparql</a>> {<br></br><br></br>    ?car rdfs:label ?taggedname ;<br></br>         dbo:location | dbo:locationCountry ?location .<br></br><br></br>    ?location rdf:type dbo:Country ;<br></br>              rdfs:label ?lname ;<br></br>              dbp:populationCensus | dbo:populationTotal ?pop .<br></br><br></br>    FILTER (LANG(?lname) = "en")<br></br>}}<br></br>}
```

The first thing we do is replace CONSTRUCT with INSERT as we now want to ingest the returned graph into our repository.

The next and final thing we must do is nest the entire WHERE clause into a second SERVICE tag. This time however, the service endpoint is the endpoint you copied at the end of the construction section.

This constructs the graph and inserts it into your repository!

> It should be a much larger graph but the messiness of DBpedia strikes again! Many car manufacturers are connected to the string label of their location and not the entity. Therefore, the locations do not have a population and are consequently not returned.

We started with a small .csv of car manufacturer names so lets explore this graph we now have.

### Exploring the New Graph

If we head to the “Explore” tab and view Japan for example, we can see our data.

<figure>![](https://cdn-images-1.medium.com/max/1024/1*Xyx5dMIZr73dLPgdOxEnoQ.png)</figure>Japan has the attached type dbo:Country, label, population and has seven car manufacturers.

There is no point in linking data if we cannot gain further insight so lets head to the “SPARQL” tab of the workbench.

<figure>![](https://cdn-images-1.medium.com/max/1024/1*ThleInG5v4qk64PLSkNvZw.png)</figure>In this screenshot we can see the results of the below query. This query returns each country alongside the number of people per car manufacturer in that country.

There is nothing new in this query if you have read my [SPARQL introduction](https://medium.com/wallscope/constructing-sparql-queries-ca63b8b9ac02). I have used the MAX population as some countries have two attached populations due to DBpedia.

```
PREFIX rdf: <<a href="http://www.w3.org/1999/02/22-rdf-syntax-ns#">http://www.w3.org/1999/02/22-rdf-syntax-ns#</a>><br></br>PREFIX rdfs: <<a href="http://www.w3.org/2000/01/rdf-schema#">http://www.w3.org/2000/01/rdf-schema#</a>><br></br>PREFIX dbo: <<a href="http://dbpedia.org/ontology/">http://dbpedia.org/ontology/</a>><br></br>PREFIX dbp: <<a href="http://dbpedia.org/property/">http://dbpedia.org/property/</a>>
```

```
SELECT ?name ((MAX(?pop) / COUNT(DISTINCT ?companies)) AS ?result)<br></br>WHERE {<br></br>    ?companies rdf:type dbo:Company ;<br></br>               dbo:location ?location .<br></br><br></br>    ?location rdf:type dbo:Country ;<br></br>              dbp:populationCensus ?pop ;<br></br>              rdfs:label ?name .<br></br>}<br></br>GROUP BY ?name<br></br>ORDER BY DESC (?result)
```

In the screenshot above you can see that the results (ordered by result in descending order) are:

- Indonesia
- Pakistan
- India
- China

India of course has a much larger population than Indonesia but also has a lot more car manufacturers (as shown below).

> If you were a car manufacturer in Asia, Indonesia might be a good market to target for export as it has a high population but very little local competition.

<figure>![](https://cdn-images-1.medium.com/max/1024/1*41vcqAXP80eu4Q-Xx2Hm_Q.png)</figure>### Conclusion

We started with a small list of car manufacturer names but, by using GraphDB and DBpedia, we managed to extend this into a small graph that we could gain actual insight from.

Of course, this example is not entirely useful but perhaps you have a list of local areas or housing statistics that you want to reconcile with mapping or government linked open data. This can be done using the above approach to help you or your business gain further insight that you could not have otherwise identified.

![](https://medium.com/_/stat?event=post.clientViewed&referrerSource=full_rss&postId=cd2796d2870b)- - - - - -

[Linked Data Reconciliation in GraphDB](https://medium.com/wallscope/linked-data-reconciliation-in-graphdb-cd2796d2870b) was originally published in [Wallscope](https://medium.com/wallscope) on Medium, where people are continuing the conversation by highlighting and responding to this story.