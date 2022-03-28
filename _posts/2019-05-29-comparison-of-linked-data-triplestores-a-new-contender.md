---
id: 990
title: 'Comparison of Linked Data Triplestores: A New Contender'
date: '2019-05-29T13:50:00+01:00'
author: 'Angus Addlesee'
excerpt: '<h4>First Impressions of RDFox while the Benchmark is Developed</h4><blockquote><strong>Note:</strong> This article is <strong>not</strong> sponsored. <a href="https://www.oxfordsemantic.tech/">Oxford Semantic Technologies</a> let me try out the new version of RDFox and are keen to be part of the future benchmark.</blockquote><p>After reading some of my <a href="https://medium.com/@addlesee">previous articles</a>, <a href="https://www.oxfordsemantic.tech/">Oxford Semantic Technologies</a> (OST) got in touch and asked if I would like to try out their triplestore called&nbsp;RDFox.</p><p>In this article I will share my thoughts and why I am now excited to see how they do in the future benchmark.</p><p>They have just released a page on which you can <a href="https://www.oxfordsemantic.tech/request-eval">request your own evaluation license</a> to try it yourself.</p><h3>Contents</h3><p><strong>Brief Benchmark Catch-up<br>How I Tested RDFox<br>First Impressions<br>Results<br>Conclusion</strong></p><figure><img alt="" src="https://cdn-images-1.medium.com/max/960/0*Olhw85Db-iCzME6z.jpg"><figcaption><a href="https://pixabay.com/de/illustrations/netzwerk-internet-kommunikation-3357642/">source</a></figcaption></figure><h3>Brief Benchmark Catch-up</h3><p>In December I wrote a <a href="https://medium.com/wallscope/comparing-linked-data-triplestores-ebfac8c3ad4f">comparison</a> of existing triplestores on a tiny dataset. I quickly learned that there were many flaws in my methodology for the results to be truly comparable.</p><p>In February I then wrote a <a href="https://medium.com/wallscope/comparison-of-linked-data-triplestores-developing-the-methodology-e87771cb3011?source=friends_link&amp;sk=69ab0d1ab9cc91554967332fa1a2ca2c">follow up</a> in which I describe many of the flaws and listed many of the details that I will have to pay attention to while developing an actual benchmark.</p><p>This benchmark is currently in development. I am now working with developers, working with academics and talking with a high-performance computing centre to give us access to the infrastructure needed to run at&nbsp;scale.</p><h3>How I Tested&nbsp;RDFox</h3><p>In the above articles I evaluated five triplestores. They were (in alphabetical order) <a href="https://twitter.com/CamSemantics">AnzoGraph</a>, <a href="https://twitter.com/BlazeGraph">Blazegraph</a>, <a href="https://twitter.com/OntotextGraphDB">GraphDB</a>, <a href="https://twitter.com/StardogHQ">Stardog</a> and <a href="https://twitter.com/OpenLink">Virtuoso</a>. I would like to include all of these in the future benchmark and now RDFox as&nbsp;well.</p><p>Obviously my previous evaluations are not completely fair comparisons (hence the development of the benchmark) but the last one can be used to get an idea of whether RDFox can compete with the&nbsp;others.</p><p>For that reason, I loaded the same data and ran the same queries as in my <a href="https://medium.com/wallscope/comparison-of-linked-data-triplestores-developing-the-methodology-e87771cb3011?source=friends_link&amp;sk=69ab0d1ab9cc91554967332fa1a2ca2c">larger comparison</a> to see how RDFox fared. I of course kept all other variables the same such as the machine, using the CLI to query, same number of warm up and hot runs,&nbsp;etc&hellip;</p><h3>First Impressions</h3><p>RDFox is very easy to use and well-documented. You can initialise it with custom scripts which is extremely useful as I could start RDFox, load all my gzipped turtle files in parallel, run all my warm up queries and run all my hot queries with one&nbsp;command.</p><p>RDFox is an in-memory solution which explains many of the differences in results but they also have a very nice rule system that can be used to precompute results that are used in later queries. These rules are not evaluated when you send a query but in&nbsp;advance.</p><p>This allows them to be used to automatically keep consistency of your data as it is added or removed. The rules themselves can even be added or removed during the lifetime of the database.</p><blockquote><strong>Note</strong>: Queries 3 and 6 use these custom rules. I highlight this on the relevant queries and this is one of the reasons I didn&rsquo;t just add them to the last&nbsp;article.</blockquote><p>You can use these rules for a number of things, for example to precompute alternate property paths (If you are unfamiliar with those then I cover them in this <a href="https://medium.com/wallscope/constructing-more-advanced-sparql-queries-72d5ade1eedc">SPARQL tutorial</a>). You could do this by defining a rule that example:predicate represents example:pred1 and example:pred2 so&nbsp;that:</p><pre>SELECT ?s ?o<br>WHERE {<br>  ?s example:predicate ?o .<br>}</pre><p>This would return the&nbsp;triples:</p><pre>person:A example:pred1 colour:blue .<br>person:A example:pred2 colour:green .<br>person:B example:pred2 colour:brown .<br>person:C example:pred1 colour:grey .</pre><p>Which make the use of alternate property paths less necessary.</p><p>With all that&hellip; let&rsquo;s see how RDFox performs.</p><h3>Results</h3><blockquote>Each of the below charts compares RDFox to the averages of the others. I exclude outliers where applicable.</blockquote><h4>Loading</h4><p>Right off the bat, RDFox was the fastest at loading which was a huge surprise as AnzoGraph was significantly faster than the others originally (184667ms).</p><p>Even if I exclude Blazegraph and GraphDB (which were significantly slower at loading than the others), you can see that RDFox was very&nbsp;fast:</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/600/1*uDl2GcTp-kvwjZ1MdGZffA.png"><figcaption>Others = AnzoGraph, Stardog and&nbsp;Virtuoso</figcaption></figure><blockquote><strong>Note</strong>: I have added who the others are as footnotes to each chart. This is so that the images are not mistaken for fair comparison results (if they showed up in a Google image search for example).</blockquote><p>RDFox and AnzoGraph are much newer triplestores which may be why they are so much faster at loading than the others. I am very excited to see how these speeds are impacted as we scale the number of triples we load in the benchmark.</p><h4>Queries</h4><p>Overall I am very impressed with RDFox&rsquo;s performance with these&nbsp;queries.</p><blockquote>It is important to note however that the other&rsquo;s results have been public for a while. I ran these queries on the newest version of RDFox <strong>AND the previous version</strong> and did not notice any significant optimisation on these particular queries. These published results are of course from the latest&nbsp;version.</blockquote><p><strong>Query 1:</strong></p><p>This query is very simple and just counts the number of relationships in the&nbsp;graph.</p><pre>SELECT (COUNT(*) AS ?triples)<br>WHERE {<br>  ?s ?p ?o .<br>}</pre><p>RDFox was the second slowest to do this but as mentioned in the <a href="https://medium.com/wallscope/comparison-of-linked-data-triplestores-developing-the-methodology-e87771cb3011?source=friends_link&amp;sk=69ab0d1ab9cc91554967332fa1a2ca2c">previous article</a>, optimisations on this query often reduce correctness.</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/600/1*Y-wH-s6znwrcIsPEnjG4gA.png"><figcaption>Faster = AnzoGraph, Blazegraph, Stardog and Virtuoso. Slower =&nbsp;GraphDB</figcaption></figure><p><strong>Query 2:</strong></p><p>This query returns a list of 1000 settlement names which have airports with identification numbers.</p><pre>PREFIX dbp: &lt;<a href="http://dbpedia.org/property/">http://dbpedia.org/property/</a>&gt;<br>PREFIX dbo: &lt;<a href="http://dbpedia.org/ontology/">http://dbpedia.org/ontology/</a>&gt;<br>PREFIX rdfs: &lt;<a href="http://www.w3.org/2000/01/rdf-schema#">http://www.w3.org/2000/01/rdf-schema#</a>&gt;<br>PREFIX foaf: &lt;<a href="http://xmlns.com/foaf/0.1/">http://xmlns.com/foaf/0.1/</a>&gt;</pre><pre>SELECT DISTINCT ?v WHERE {<br>  { ?v2 a dbo:Settlement ;<br>        rdfs:label ?v .<br>    ?v6 a dbo:Airport . }<br>  { ?v6 dbo:city ?v2 . }<br>  UNION<br>    { ?v6 dbo:location ?v2 . }<br>  { ?v6 dbp:iata ?v5 . }<br>  UNION<br>    { ?v6 dbo:iataLocationIdentifier ?v5 . }<br>  OPTIONAL { ?v6 foaf:homepage ?v7 . }<br>  OPTIONAL { ?v6 dbp:nativename ?v8 . }<br>} LIMIT 1000</pre><p>RDFox was the fastest to complete this query by a fairly significant margin and this is likely because it is an in-memory solution. GraphDB was the second fastest in 29.6ms and then Virtuoso in&nbsp;88.2ms.</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/600/1*R6SjpBDXQuVifmrbCYnHLA.png"><figcaption>Others = Blazegraph, GraphDB, Stardog and&nbsp;Virtuoso</figcaption></figure><p>I would like to reiterate that there are several problems with these queries that will be solved in the benchmark. For example, this query has a LIMIT but no ORDER BY which is highly unrealistic.</p><p><strong>Query 3:</strong></p><p>This query nests query 2 to grab information about the 1,000 settlements returned&nbsp;above.</p><blockquote>You will notice that this query is slightly different to query 3 in the <a href="https://medium.com/wallscope/comparison-of-linked-data-triplestores-developing-the-methodology-e87771cb3011?source=friends_link&amp;sk=69ab0d1ab9cc91554967332fa1a2ca2c">original&nbsp;article</a>.</blockquote><pre>PREFIX dbp: &lt;<a href="http://dbpedia.org/property/">http://dbpedia.org/property/</a>&gt;<br>PREFIX dbo: &lt;<a href="http://dbpedia.org/ontology/">http://dbpedia.org/ontology/</a>&gt;<br>PREFIX rdfs: &lt;<a href="http://www.w3.org/2000/01/rdf-schema#">http://www.w3.org/2000/01/rdf-schema#</a>&gt;<br>PREFIX foaf: &lt;<a href="http://xmlns.com/foaf/0.1/">http://xmlns.com/foaf/0.1/</a>&gt;</pre><pre>SELECT ?v ?v2 ?v5 ?v6 ?v7 ?v8 WHERE {<br>  ?v2 a dbo:Settlement;<br>      rdfs:label ?v.<br>  ?v6 a dbo:Airport.<br>  { ?v6 dbo:city ?v2. }<br>  UNION<br>  { ?v6 dbo:location ?v2. }<br>  { ?v6 dbp:iata ?v5. }<br>  UNION<br>  { ?v6 dbo:iataLocationIdentifier ?v5. }<br>  OPTIONAL { ?v6 foaf:homepage ?v7. }<br>  OPTIONAL { ?v6 dbp:nativename ?v8. }<br>  {<br>    FILTER(EXISTS{ SELECT ?v WHERE {<br>      ?v2 a dbo:Settlement;<br>          rdfs:label ?v.<br>      ?v6 a dbo:Airport.<br>      { ?v6 dbo:city ?v2. }<br>      UNION<br>      { ?v6 dbo:location ?v2. }<br>      { ?v6 dbp:iata ?v5. }<br>      UNION<br>      { ?v6 dbo:iataLocationIdentifier ?v5. }<br>      OPTIONAL { ?v6 foaf:homepage ?v7. }<br>      OPTIONAL { ?v6 dbp:nativename ?v8. }<br>    }<br>    LIMIT 1000<br>    })<br>  }<br>}</pre><p>RDFox was again the fastest to complete query 3 but it is important to reiterate that this query was modified slightly so that it could run on RDFox. The only other query that has the same issue is query&nbsp;6.</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/600/1*NYk5GTIdYHW3PBSJUTKitA.png"><figcaption>Others = Blazegraph, GraphDB, Stardog and&nbsp;Virtuoso</figcaption></figure><p>The results of query 2 and 3 are very similar of course as query 2 is nested within query&nbsp;2.</p><p><strong>Query 4:</strong></p><p>The two queries above were similar but query 4 is a lot more mathematical.</p><pre>PREFIX dbo: &lt;http://dbpedia.org/ontology/&gt;<br>PREFIX geo: &lt;http://www.w3.org/2003/01/geo/wgs84_pos#&gt;<br>SELECT (ROUND(?x/?y) AS ?result) WHERE {  <br>  {SELECT (CEIL(?a + ?b) AS ?x) WHERE {<br>    {SELECT (AVG(?abslat) AS ?a) WHERE {<br>    ?s1 geo:lat ?lat .<br>    BIND(ABS(?lat) AS ?abslat)<br>    }}<br>    {SELECT (SUM(?rv) AS ?b) WHERE {<br>    ?s2 dbo:volume ?volume .<br>    BIND((RAND() * ?volume) AS ?rv)<br>    }}<br>  }}<br><br>  {SELECT ((FLOOR(?c + ?d)) AS ?y) WHERE {<br>      {SELECT ?c WHERE {<br>        BIND(MINUTES(NOW()) AS ?c)<br>      }}<br>      {SELECT (AVG(?width) AS ?d) WHERE {<br>        ?s3 dbo:width ?width .<br>        FILTER(?width &gt; 50)<br>      }}<br>  }}<br>}</pre><p>AnzoGraph was the quickest to complete query 4 with RDFox in second&nbsp;place.</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/600/1*ZbezXopvH4Uygj3qHnxbgg.png"><figcaption>Faster = AnzoGraph. Slower = Blazegraph, Stardog and&nbsp;Virtuoso</figcaption></figure><p>Virtuoso was the third fastest to complete this query in a time of&nbsp;519.5ms.</p><p>As with all these queries, they do not contain random seeds so I have made sure to include mathematical queries in the benchmark.</p><p><strong>Query 5:</strong></p><p>This query focuses on strings rather than mathematical function. It essentially grabs all labels containing the string &lsquo;venus&rsquo;, all comments containing &lsquo;sleep&rsquo; and all abstracts containing &lsquo;gluten&rsquo;. It then constructs an entity and attaches all of these to&nbsp;it.</p><blockquote>I use a CONSTRUCT query here. I wrote a second SPARQL tutorial, which covers constructs, called <a href="https://medium.com/wallscope/constructing-more-advanced-sparql-queries-72d5ade1eedc">Constructing More Advanced SPARQL Queries</a> for those that&nbsp;need.</blockquote><pre>PREFIX ex: &lt;http://wallscope.co.uk/resource/example/&gt;<br>PREFIX dbo: &lt;http://dbpedia.org/ontology/&gt;<br>PREFIX rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt;<br>CONSTRUCT {<br>  ex:notglutenfree rdfs:label ?label ;<br>                   rdfs:comment ?sab ;<br>                   dbo:abstract ?lab .<br>} WHERE {<br>  {?s1 rdfs:label ?label .<br>  FILTER (REGEX(lcase(?label), ''venus''))<br>  } UNION<br>  {?s2 rdfs:comment ?sab .<br>  FILTER (REGEX(lcase(?sab), ''sleep''))<br>  } UNION<br>  {?s3 dbo:abstract ?lab .<br>  FILTER (REGEX(lcase(?lab), ''gluten''))<br>  }<br>}</pre><p>As discussed in the <a href="https://medium.com/wallscope/comparison-of-linked-data-triplestores-developing-the-methodology-e87771cb3011?source=friends_link&amp;sk=69ab0d1ab9cc91554967332fa1a2ca2c">previous post</a>, it is uncommon to use REGEX queries if you can run a full text index query on the triplestore. AnzoGraph and RDFox are the only two that do not have built in full indexes, hence these&nbsp;results:</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/600/1*dPWhyqiZbYEKZsfnVnkYdQ.png"><figcaption>Faster = AnzoGraph. Slower = Blazegraph, GraphDB, Stardog and&nbsp;Virtuoso</figcaption></figure><p>AnzoGraph is a little faster than RDFox to complete this query but the two of them are significantly faster than the rest. This is of course because you would use the full text index capabilities of the other triplestores.</p><p>If we instead run full text index queries, they are significantly faster than&nbsp;RDFox.</p><blockquote><strong>Note</strong>: To ensure clarity, in this chart RDFox was running the REGEX query as it does not have full text index functionality.</blockquote><figure><img alt="" src="https://cdn-images-1.medium.com/max/600/1*cbkmavEir1HEmxQijWfVmg.png"><figcaption>Others = Blazegraph, GraphDB, Stardog and&nbsp;Virtuoso</figcaption></figure><p>Whenever I can run a full text index query I will because of the serious performance boost. Therefore this chart is definitely fairer on the other triplestores.</p><p><strong>Query 6:</strong></p><p>This query finds all soccer players that are born in a country with more than 10 million inhabitants, who played as goalkeeper for a club that has a stadium with more than 30.000 seats and the club country is different from the birth&nbsp;country.</p><blockquote><strong>Note</strong>: This is the second, and final, query that is modified slightly for RDFox. The original query contained both alternate and recurring property paths which were handled by their rule&nbsp;system.</blockquote><pre>PREFIX dbo: &lt;<a href="http://dbpedia.org/ontology/">http://dbpedia.org/ontology/</a>&gt;<br>PREFIX dbp: &lt;<a href="http://dbpedia.org/property/">http://dbpedia.org/property/</a>&gt;<br>PREFIX : &lt;<a href="http://ost.com/">http://ost.com/</a>&gt;</pre><pre>SELECT DISTINCT ?soccerplayer ?countryOfBirth ?team ?countryOfTeam ?stadiumcapacity<br>{ <br>?soccerplayer a dbo:SoccerPlayer ;<br>   :position &lt;<a href="http://dbpedia.org/resource/Goalkeeper_(association_football)">http://dbpedia.org/resource/Goalkeeper_(association_football)</a>&gt; ;<br>   :countryOfBirth ?countryOfBirth ;<br>   dbo:team ?team .<br>   ?team dbo:capacity ?stadiumcapacity ; dbo:ground ?countryOfTeam . <br>   ?countryOfBirth a dbo:Country ; dbo:populationTotal ?population .<br>   ?countryOfTeam a dbo:Country .<br>FILTER (?countryOfTeam != ?countryOfBirth)<br>FILTER (?stadiumcapacity &gt; 30000)<br>FILTER (?population &gt; 10000000)<br>} order by ?soccerplayer</pre><blockquote>If interested in alternate property paths, I cover them in my article called <a href="https://medium.com/wallscope/constructing-more-advanced-sparql-queries-72d5ade1eedc">Constructing More Advanced SPARQL&nbsp;Queries</a>.</blockquote><p>RDFox was fastest again to complete query 6. This speed is probably down to the rule system changes as some of the query is essentially done beforehand.</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/600/1*Z1h5xjJEXTmazeT72jk_0Q.png"><figcaption>Others = Blazegraph, GraphDB, Stardog and&nbsp;Virtuoso</figcaption></figure><p>For the above reason, RDFox&rsquo;s rule system will have to be investigated thoroughly before the benchmark.</p><p>Virtuoso was the second fastest to complete this query in a time of 54.9ms which is still very fast compared to the&nbsp;average.</p><p><strong>Query 7:</strong></p><p>Finally, this query finds all people born in Berlin before&nbsp;1900.</p><pre>PREFIX xsd: &lt;<a href="http://www.w3.org/2001/XMLSchema#">http://www.w3.org/2001/XMLSchema#</a>&gt;<br>PREFIX foaf: &lt;<a href="http://xmlns.com/foaf/0.1/">http://xmlns.com/foaf/0.1/</a>&gt;<br>PREFIX : &lt;<a href="http://dbpedia.org/resource/">http://dbpedia.org/resource/</a>&gt;<br>PREFIX dbo: &lt;<a href="http://dbpedia.org/ontology/">http://dbpedia.org/ontology/</a>&gt;</pre><pre>SELECT ?name ?birth ?death ?person<br>WHERE {<br> ?person dbo:birthPlace :Berlin .<br> ?person dbo:birthDate ?birth .<br> ?person foaf:name ?name .<br> ?person dbo:deathDate ?death .<br> FILTER (?birth &lt; "1900-01-01"^^xsd:date)<br> }<br> ORDER BY ?name</pre><p>Finishing with a very simple query and no custom rules (like queries 3 and 6), RDFox was once again the fastest to complete this&nbsp;query.</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/600/1*CCrLBjVj2UinPZjSzyFH1g.png"><figcaption>Others = AnzoGraph, Blazegraph, GraphDB, Stardog and&nbsp;Virtuoso</figcaption></figure><p>In this case, the average includes every other triplestore as there were no real outliers. Virtuoso was again the second fastest and completed query 7 in 20.2ms so relatively fast compared to the average. This speed difference is again likely due to the fact that RDFox is an in-memory solution.</p><h3>Conclusion</h3><p>To reiterate, this is not a sound comparison so I cannot conclude that RDFox is better or worse than triplestore X and Y. What I can conclude is&nbsp;this:</p><blockquote>RDFox can definitely compete with the other major triplestores and initial results suggest that they have the potential to be one of the top performers in our benchmark.</blockquote><p>I can also say that RDFox is very easy to use, well documented and the rule system gives the opportunity for users to add custom reasoning very&nbsp;easily.</p><p>If you want to try it for yourself, you can <a href="https://www.oxfordsemantic.tech/request-eval">request a license&nbsp;here</a>.</p><blockquote><strong>Again to summarise the notes throughout</strong>: RDFox did <strong>not</strong> sponsor this article. They did know the other&rsquo;s results since I published my <a href="https://medium.com/wallscope/comparison-of-linked-data-triplestores-developing-the-methodology-e87771cb3011?source=friends_link&amp;sk=69ab0d1ab9cc91554967332fa1a2ca2c">last article</a> but I did test the previous version of RDFox also and didn&rsquo;t notice any significant optimisation. The rule system makes queries 3 and 6 difficult to compare but that will be investigated before running the benchmark.</blockquote><img src="https://medium.com/_/stat?event=post.clientViewed&amp;referrerSource=full_rss&amp;postId=c62ae04901d3" width="1" height="1"><hr><p><a href="https://medium.com/wallscope/comparison-of-linked-data-triplestores-a-new-contender-c62ae04901d3">Comparison of Linked Data Triplestores: A New Contender</a> was originally published in <a href="https://medium.com/wallscope">Wallscope</a> on Medium, where people are continuing the conversation by highlighting and responding to this story.</p>'
layout: post
guid: 'https://medium.com/p/c62ae04901d3'
permalink: 'https://medium.com/wallscope/comparison-of-linked-data-triplestores-a-new-contender-c62ae04901d3?source=rss-7f06284203ea------2'
syndication_source:
    - 'Stories by Angus Addlesee on Medium'
syndication_source_uri:
    - 'https://medium.com/@addlesee?source=rss-7f06284203ea------2'
syndication_source_id:
    - 'https://medium.com/feed/@addlesee'
syndication_feed:
    - 'https://medium.com/feed/@addlesee'
syndication_feed_id:
    - '3'
syndication_permalink:
    - 'https://medium.com/wallscope/comparison-of-linked-data-triplestores-a-new-contender-c62ae04901d3?source=rss-7f06284203ea------2'
syndication_item_hash:
    - 0f27d14717a918121d0b5178a65eb8d7
    - 006d43e8b52d63b39c9c6812655504b5
    - 006d43e8b52d63b39c9c6812655504b5
    - 0030dc55abd1868ebec9762867591cb2
    - c0034f5b940738caed52d66ae7cd5ef2
categories:
    - data-science
    - database
    - 'Linked Data'
    - rdf
    - semanticweb
---

#### First Impressions of RDFox while the Benchmark is Developed

> **Note:** This article is **not** sponsored. [Oxford Semantic Technologies](https://www.oxfordsemantic.tech/) let me try out the new version of RDFox and are keen to be part of the future benchmark.

After reading some of my [previous articles](https://medium.com/@addlesee), [Oxford Semantic Technologies](https://www.oxfordsemantic.tech/) (OST) got in touch and asked if I would like to try out their triplestore called RDFox. In this article I will share my thoughts and why I am now excited to see how they do in the future benchmark. They have just released a page on which you can [request your own evaluation license](https://www.oxfordsemantic.tech/request-eval) to try it yourself. ### Contents

**Brief Benchmark Catch-up How I Tested RDFox First Impressions Results Conclusion**<figure>![](https://cdn-images-1.medium.com/max/960/0*Olhw85Db-iCzME6z.jpg)<figcaption>[source](https://pixabay.com/de/illustrations/netzwerk-internet-kommunikation-3357642/)</figcaption></figure>### Brief Benchmark Catch-up

In December I wrote a [comparison](https://medium.com/wallscope/comparing-linked-data-triplestores-ebfac8c3ad4f) of existing triplestores on a tiny dataset. I quickly learned that there were many flaws in my methodology for the results to be truly comparable. In February I then wrote a [follow up](https://medium.com/wallscope/comparison-of-linked-data-triplestores-developing-the-methodology-e87771cb3011?source=friends_link&sk=69ab0d1ab9cc91554967332fa1a2ca2c) in which I describe many of the flaws and listed many of the details that I will have to pay attention to while developing an actual benchmark. This benchmark is currently in development. I am now working with developers, working with academics and talking with a high-performance computing centre to give us access to the infrastructure needed to run at scale. ### How I Tested RDFox

In the above articles I evaluated five triplestores. They were (in alphabetical order) [AnzoGraph](https://twitter.com/CamSemantics), [Blazegraph](https://twitter.com/BlazeGraph), [GraphDB](https://twitter.com/OntotextGraphDB), [Stardog](https://twitter.com/StardogHQ) and [Virtuoso](https://twitter.com/OpenLink). I would like to include all of these in the future benchmark and now RDFox as well. Obviously my previous evaluations are not completely fair comparisons (hence the development of the benchmark) but the last one can be used to get an idea of whether RDFox can compete with the others. For that reason, I loaded the same data and ran the same queries as in my [larger comparison](https://medium.com/wallscope/comparison-of-linked-data-triplestores-developing-the-methodology-e87771cb3011?source=friends_link&sk=69ab0d1ab9cc91554967332fa1a2ca2c) to see how RDFox fared. I of course kept all other variables the same such as the machine, using the CLI to query, same number of warm up and hot runs, etc… ### First Impressions

RDFox is very easy to use and well-documented. You can initialise it with custom scripts which is extremely useful as I could start RDFox, load all my gzipped turtle files in parallel, run all my warm up queries and run all my hot queries with one command. RDFox is an in-memory solution which explains many of the differences in results but they also have a very nice rule system that can be used to precompute results that are used in later queries. These rules are not evaluated when you send a query but in advance. This allows them to be used to automatically keep consistency of your data as it is added or removed. The rules themselves can even be added or removed during the lifetime of the database. > **Note**: Queries 3 and 6 use these custom rules. I highlight this on the relevant queries and this is one of the reasons I didn’t just add them to the last article.

You can use these rules for a number of things, for example to precompute alternate property paths (If you are unfamiliar with those then I cover them in this [SPARQL tutorial](https://medium.com/wallscope/constructing-more-advanced-sparql-queries-72d5ade1eedc)). You could do this by defining a rule that example:predicate represents example:pred1 and example:pred2 so that: ```
SELECT ?s ?o
WHERE {
  ?s example:predicate ?o .
}
```

This would return the triples: ```
person:A example:pred1 colour:blue .
person:A example:pred2 colour:green .
person:B example:pred2 colour:brown .
person:C example:pred1 colour:grey .
```

Which make the use of alternate property paths less necessary. With all that… let’s see how RDFox performs. ### Results

> Each of the below charts compares RDFox to the averages of the others. I exclude outliers where applicable.

#### Loading

Right off the bat, RDFox was the fastest at loading which was a huge surprise as AnzoGraph was significantly faster than the others originally (184667ms). Even if I exclude Blazegraph and GraphDB (which were significantly slower at loading than the others), you can see that RDFox was very fast: <figure>![](https://cdn-images-1.medium.com/max/600/1*uDl2GcTp-kvwjZ1MdGZffA.png)<figcaption>Others = AnzoGraph, Stardog and Virtuoso</figcaption></figure>> **Note**: I have added who the others are as footnotes to each chart. This is so that the images are not mistaken for fair comparison results (if they showed up in a Google image search for example).

RDFox and AnzoGraph are much newer triplestores which may be why they are so much faster at loading than the others. I am very excited to see how these speeds are impacted as we scale the number of triples we load in the benchmark. #### Queries

Overall I am very impressed with RDFox’s performance with these queries. > It is important to note however that the other’s results have been public for a while. I ran these queries on the newest version of RDFox **AND the previous version** and did not notice any significant optimisation on these particular queries. These published results are of course from the latest version.

**Query 1:**This query is very simple and just counts the number of relationships in the graph. ```
SELECT (COUNT(*) AS ?triples)
WHERE {
  ?s ?p ?o .
}
```

RDFox was the second slowest to do this but as mentioned in the [previous article](https://medium.com/wallscope/comparison-of-linked-data-triplestores-developing-the-methodology-e87771cb3011?source=friends_link&sk=69ab0d1ab9cc91554967332fa1a2ca2c), optimisations on this query often reduce correctness. <figure>![](https://cdn-images-1.medium.com/max/600/1*Y-wH-s6znwrcIsPEnjG4gA.png)<figcaption>Faster = AnzoGraph, Blazegraph, Stardog and Virtuoso. Slower = GraphDB</figcaption></figure>**Query 2:**This query returns a list of 1000 settlement names which have airports with identification numbers. ```
PREFIX dbp: <<a href="http://dbpedia.org/property/">http://dbpedia.org/property/</a>>
PREFIX dbo: <<a href="http://dbpedia.org/ontology/">http://dbpedia.org/ontology/</a>>
PREFIX rdfs: <<a href="http://www.w3.org/2000/01/rdf-schema#">http://www.w3.org/2000/01/rdf-schema#</a>>
PREFIX foaf: <<a href="http://xmlns.com/foaf/0.1/">http://xmlns.com/foaf/0.1/</a>>
```

```
SELECT DISTINCT ?v WHERE {
  { ?v2 a dbo:Settlement ;
        rdfs:label ?v .
    ?v6 a dbo:Airport . }
  { ?v6 dbo:city ?v2 . }
  UNION
    { ?v6 dbo:location ?v2 . }
  { ?v6 dbp:iata ?v5 . }
  UNION
    { ?v6 dbo:iataLocationIdentifier ?v5 . }
  OPTIONAL { ?v6 foaf:homepage ?v7 . }
  OPTIONAL { ?v6 dbp:nativename ?v8 . }
} LIMIT 1000
```

RDFox was the fastest to complete this query by a fairly significant margin and this is likely because it is an in-memory solution. GraphDB was the second fastest in 29.6ms and then Virtuoso in 88.2ms. <figure>![](https://cdn-images-1.medium.com/max/600/1*R6SjpBDXQuVifmrbCYnHLA.png)<figcaption>Others = Blazegraph, GraphDB, Stardog and Virtuoso</figcaption></figure>I would like to reiterate that there are several problems with these queries that will be solved in the benchmark. For example, this query has a LIMIT but no ORDER BY which is highly unrealistic. **Query 3:**This query nests query 2 to grab information about the 1,000 settlements returned above. > You will notice that this query is slightly different to query 3 in the [original article](https://medium.com/wallscope/comparison-of-linked-data-triplestores-developing-the-methodology-e87771cb3011?source=friends_link&sk=69ab0d1ab9cc91554967332fa1a2ca2c).

```
PREFIX dbp: <<a href="http://dbpedia.org/property/">http://dbpedia.org/property/</a>>
PREFIX dbo: <<a href="http://dbpedia.org/ontology/">http://dbpedia.org/ontology/</a>>
PREFIX rdfs: <<a href="http://www.w3.org/2000/01/rdf-schema#">http://www.w3.org/2000/01/rdf-schema#</a>>
PREFIX foaf: <<a href="http://xmlns.com/foaf/0.1/">http://xmlns.com/foaf/0.1/</a>>
```

```
SELECT ?v ?v2 ?v5 ?v6 ?v7 ?v8 WHERE {
  ?v2 a dbo:Settlement;
      rdfs:label ?v.
  ?v6 a dbo:Airport.
  { ?v6 dbo:city ?v2. }
  UNION
  { ?v6 dbo:location ?v2. }
  { ?v6 dbp:iata ?v5. }
  UNION
  { ?v6 dbo:iataLocationIdentifier ?v5. }
  OPTIONAL { ?v6 foaf:homepage ?v7. }
  OPTIONAL { ?v6 dbp:nativename ?v8. }
  {
    FILTER(EXISTS{ SELECT ?v WHERE {
      ?v2 a dbo:Settlement;
          rdfs:label ?v.
      ?v6 a dbo:Airport.
      { ?v6 dbo:city ?v2. }
      UNION
      { ?v6 dbo:location ?v2. }
      { ?v6 dbp:iata ?v5. }
      UNION
      { ?v6 dbo:iataLocationIdentifier ?v5. }
      OPTIONAL { ?v6 foaf:homepage ?v7. }
      OPTIONAL { ?v6 dbp:nativename ?v8. }
    }
    LIMIT 1000
    })
  }
}
```

RDFox was again the fastest to complete query 3 but it is important to reiterate that this query was modified slightly so that it could run on RDFox. The only other query that has the same issue is query 6. <figure>![](https://cdn-images-1.medium.com/max/600/1*NYk5GTIdYHW3PBSJUTKitA.png)<figcaption>Others = Blazegraph, GraphDB, Stardog and Virtuoso</figcaption></figure>The results of query 2 and 3 are very similar of course as query 2 is nested within query 2. **Query 4:**The two queries above were similar but query 4 is a lot more mathematical. ```
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX geo: <http://www.w3.org/2003/01/geo/wgs84_pos#>
SELECT (ROUND(?x/?y) AS ?result) WHERE {  
  {SELECT (CEIL(?a + ?b) AS ?x) WHERE {
    {SELECT (AVG(?abslat) AS ?a) WHERE {
    ?s1 geo:lat ?lat .
    BIND(ABS(?lat) AS ?abslat)
    }}
    {SELECT (SUM(?rv) AS ?b) WHERE {
    ?s2 dbo:volume ?volume .
    BIND((RAND() * ?volume) AS ?rv)
    }}
  }}
  
  {SELECT ((FLOOR(?c + ?d)) AS ?y) WHERE {
      {SELECT ?c WHERE {
        BIND(MINUTES(NOW()) AS ?c)
      }}
      {SELECT (AVG(?width) AS ?d) WHERE {
        ?s3 dbo:width ?width .
        FILTER(?width > 50)
      }}
  }}
}
```

AnzoGraph was the quickest to complete query 4 with RDFox in second place. <figure>![](https://cdn-images-1.medium.com/max/600/1*ZbezXopvH4Uygj3qHnxbgg.png)<figcaption>Faster = AnzoGraph. Slower = Blazegraph, Stardog and Virtuoso</figcaption></figure>Virtuoso was the third fastest to complete this query in a time of 519.5ms. As with all these queries, they do not contain random seeds so I have made sure to include mathematical queries in the benchmark. **Query 5:**This query focuses on strings rather than mathematical function. It essentially grabs all labels containing the string ‘venus’, all comments containing ‘sleep’ and all abstracts containing ‘gluten’. It then constructs an entity and attaches all of these to it. > I use a CONSTRUCT query here. I wrote a second SPARQL tutorial, which covers constructs, called [Constructing More Advanced SPARQL Queries](https://medium.com/wallscope/constructing-more-advanced-sparql-queries-72d5ade1eedc) for those that need.

```
PREFIX ex: <http://wallscope.co.uk/resource/example/>
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
CONSTRUCT {
  ex:notglutenfree rdfs:label ?label ;
                   rdfs:comment ?sab ;
                   dbo:abstract ?lab .
} WHERE {
  {?s1 rdfs:label ?label .
  FILTER (REGEX(lcase(?label), 'venus'))
  } UNION
  {?s2 rdfs:comment ?sab .
  FILTER (REGEX(lcase(?sab), 'sleep'))
  } UNION
  {?s3 dbo:abstract ?lab .
  FILTER (REGEX(lcase(?lab), 'gluten'))
  }
}
```

As discussed in the [previous post](https://medium.com/wallscope/comparison-of-linked-data-triplestores-developing-the-methodology-e87771cb3011?source=friends_link&sk=69ab0d1ab9cc91554967332fa1a2ca2c), it is uncommon to use REGEX queries if you can run a full text index query on the triplestore. AnzoGraph and RDFox are the only two that do not have built in full indexes, hence these results: <figure>![](https://cdn-images-1.medium.com/max/600/1*dPWhyqiZbYEKZsfnVnkYdQ.png)<figcaption>Faster = AnzoGraph. Slower = Blazegraph, GraphDB, Stardog and Virtuoso</figcaption></figure>AnzoGraph is a little faster than RDFox to complete this query but the two of them are significantly faster than the rest. This is of course because you would use the full text index capabilities of the other triplestores. If we instead run full text index queries, they are significantly faster than RDFox. > **Note**: To ensure clarity, in this chart RDFox was running the REGEX query as it does not have full text index functionality.

<figure>![](https://cdn-images-1.medium.com/max/600/1*cbkmavEir1HEmxQijWfVmg.png)<figcaption>Others = Blazegraph, GraphDB, Stardog and Virtuoso</figcaption></figure>Whenever I can run a full text index query I will because of the serious performance boost. Therefore this chart is definitely fairer on the other triplestores. **Query 6:**This query finds all soccer players that are born in a country with more than 10 million inhabitants, who played as goalkeeper for a club that has a stadium with more than 30.000 seats and the club country is different from the birth country. > **Note**: This is the second, and final, query that is modified slightly for RDFox. The original query contained both alternate and recurring property paths which were handled by their rule system.

```
PREFIX dbo: <<a href="http://dbpedia.org/ontology/">http://dbpedia.org/ontology/</a>>
PREFIX dbp: <<a href="http://dbpedia.org/property/">http://dbpedia.org/property/</a>>
PREFIX : <<a href="http://ost.com/">http://ost.com/</a>>
```

```
SELECT DISTINCT ?soccerplayer ?countryOfBirth ?team ?countryOfTeam ?stadiumcapacity
{ 
?soccerplayer a dbo:SoccerPlayer ;
   :position <<a href="http://dbpedia.org/resource/Goalkeeper_(association_football)">http://dbpedia.org/resource/Goalkeeper_(association_football)</a>> ;
   :countryOfBirth ?countryOfBirth ;
   dbo:team ?team .
   ?team dbo:capacity ?stadiumcapacity ; dbo:ground ?countryOfTeam . 
   ?countryOfBirth a dbo:Country ; dbo:populationTotal ?population .
   ?countryOfTeam a dbo:Country .
FILTER (?countryOfTeam != ?countryOfBirth)
FILTER (?stadiumcapacity > 30000)
FILTER (?population > 10000000)
} order by ?soccerplayer
```

> If interested in alternate property paths, I cover them in my article called [Constructing More Advanced SPARQL Queries](https://medium.com/wallscope/constructing-more-advanced-sparql-queries-72d5ade1eedc).

RDFox was fastest again to complete query 6. This speed is probably down to the rule system changes as some of the query is essentially done beforehand. <figure>![](https://cdn-images-1.medium.com/max/600/1*Z1h5xjJEXTmazeT72jk_0Q.png)<figcaption>Others = Blazegraph, GraphDB, Stardog and Virtuoso</figcaption></figure>For the above reason, RDFox’s rule system will have to be investigated thoroughly before the benchmark. Virtuoso was the second fastest to complete this query in a time of 54.9ms which is still very fast compared to the average. **Query 7:**Finally, this query finds all people born in Berlin before 1900. ```
PREFIX xsd: <<a href="http://www.w3.org/2001/XMLSchema#">http://www.w3.org/2001/XMLSchema#</a>>
PREFIX foaf: <<a href="http://xmlns.com/foaf/0.1/">http://xmlns.com/foaf/0.1/</a>>
PREFIX : <<a href="http://dbpedia.org/resource/">http://dbpedia.org/resource/</a>>
PREFIX dbo: <<a href="http://dbpedia.org/ontology/">http://dbpedia.org/ontology/</a>>
```

```
SELECT ?name ?birth ?death ?person
WHERE {
 ?person dbo:birthPlace :Berlin .
 ?person dbo:birthDate ?birth .
 ?person foaf:name ?name .
 ?person dbo:deathDate ?death .
 FILTER (?birth < "1900-01-01"^^xsd:date)
 }
 ORDER BY ?name
```

Finishing with a very simple query and no custom rules (like queries 3 and 6), RDFox was once again the fastest to complete this query. <figure>![](https://cdn-images-1.medium.com/max/600/1*CCrLBjVj2UinPZjSzyFH1g.png)<figcaption>Others = AnzoGraph, Blazegraph, GraphDB, Stardog and Virtuoso</figcaption></figure>In this case, the average includes every other triplestore as there were no real outliers. Virtuoso was again the second fastest and completed query 7 in 20.2ms so relatively fast compared to the average. This speed difference is again likely due to the fact that RDFox is an in-memory solution. ### Conclusion

To reiterate, this is not a sound comparison so I cannot conclude that RDFox is better or worse than triplestore X and Y. What I can conclude is this: > RDFox can definitely compete with the other major triplestores and initial results suggest that they have the potential to be one of the top performers in our benchmark.

I can also say that RDFox is very easy to use, well documented and the rule system gives the opportunity for users to add custom reasoning very easily. If you want to try it for yourself, you can [request a license here](https://www.oxfordsemantic.tech/request-eval). > **Again to summarise the notes throughout**: RDFox did **not** sponsor this article. They did know the other’s results since I published my [last article](https://medium.com/wallscope/comparison-of-linked-data-triplestores-developing-the-methodology-e87771cb3011?source=friends_link&sk=69ab0d1ab9cc91554967332fa1a2ca2c) but I did test the previous version of RDFox also and didn’t notice any significant optimisation. The rule system makes queries 3 and 6 difficult to compare but that will be investigated before running the benchmark.

![](https://medium.com/_/stat?event=post.clientViewed&referrerSource=full_rss&postId=c62ae04901d3)- - - - - -

[Comparison of Linked Data Triplestores: A New Contender](https://medium.com/wallscope/comparison-of-linked-data-triplestores-a-new-contender-c62ae04901d3) was originally published in [Wallscope](https://medium.com/wallscope) on Medium, where people are continuing the conversation by highlighting and responding to this story.