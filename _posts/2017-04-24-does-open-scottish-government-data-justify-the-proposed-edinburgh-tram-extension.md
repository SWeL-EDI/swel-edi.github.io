---
id: 512
title: 'Does Open Scottish Government Data Justify the Proposed Edinburgh Tram Extension?'
date: '2017-04-24T01:50:13+01:00'
author: 'Rob Stewart'
layout: post
guid: 'http://www.macs.hw.ac.uk/SWeL/?p=512'
permalink: /2017/04/24/does-open-scottish-government-data-justify-the-proposed-edinburgh-tram-extension/
categories:
    - Uncategorized
---

The Scottish government provides open access to a range of official statistics about Scotland across [17 themes](http://statistics.gov.scot/def/concept/folders/themes), including crime, the economy, housing, and population growths. The portal is accessible at <http://statistics.gov.scot>.

This post uses open Scottish government data to measure the *5 year population growth in areas in close proximity to the proposed completion of [phase 1a](https://en.wikipedia.org/wiki/Proposals_for_new_tram_lines_in_Edinburgh#Line_1_.28North_Edinburgh.29) of the tram extension, from York Place to Newhaven.*

### The tram infrastructure business case

The original business case for the tram infrastructure was set out in a document *[Edinburgh Tram Draft Final Business Case](http://www.edinburgh.gov.uk/download/meetings/id/4562/edinburgh_tram_draft_final_business_case_part_1) (*The City of Edinburgh Council, December 2006). It justifies the need for a tram system using two broad arguments:

1. The predicted **growth in housing demands** for a growing population in the areas on the proposed lines:

> “Huge new developments are in the pipeline, especially on the city’s waterfront in Leith Docks and Granton. Edinburgh Waterfront is the largest brownfield development in Scotland, equivalent to a major new town in scale, with the two major development sites able to accommodate up to 29,000 new homes in the longer term (Section 3.3, Why Tram).”

2\. The tram system will encourage **economic regeneration** and **social inclusion**:

> “Without the tram, access to the major Waterfront developments will simply not be good enough. The Leith Docks proposals would have to be scaled down and the development prospects at Granton would be damaged (Section 3.3, Why Tram). Areas of \[..\] a zone around Leith Walk \[..\] are areas where socio economic status is considerably less affluent than surrounding areas and where employment, income levels and car ownership tend to be comparatively low. Opportunities for people living in these areas will be improved by direct connection via tram to the City Centre and other employment areas, including the new development in Granton, Leith and the West of the City at Edinburgh Park and the Airport (Section 1.18, Accessibility and Social Inclusion).”

This document, written 11 years ago, made various projections of population growths, particularly in the north and north east of Edinburgh. For example, it states that 24,000 new houses will be needed in Edinburgh by 2015 (Section 3.3, Why Tram). The Scottish government open data portal can be used to assess the accuracy of those projections.

### Party political views on the proposed extension

Due to well documented economic costs and major project problems, the tram stretches only as far as York Place. Edinburgh City Council are considering an extension from York Place down Leith Walk, to Newhaven. It could be partly funded by a [City Deal](http://www.edinburghnews.scotsman.com/news/city-deal-could-help-fund-edinburgh-tram-extension-to-leith-and-beyond-1-4203085). A definitive yes/no decision on the extension will be made after the local council elections take place on 4th May 2017. The Labour party are [in favour](https://d3n8a8pro7vhmx.cloudfront.net/labourclp439/pages/528/attachments/original/1490017496/ED_LAB_MANIFESTO_FIN_LR.PDF?1490017496), the SNP have recently [set conditions](http://www.edinburghnews.scotsman.com/news/politics/snp-sets-conditions-for-giving-ok-to-tram-extension-1-4415848) on their backing of the extension, whilst the Conservative party have promised to reject the business case for the extension in their [council election manifesto](https://www.edinburghconservatives.org.uk/sites/www.edinburghconservatives.org.uk/files/2017-04/Manifesto2017.pdf).

### Zones along the proposed tram extension

The long term proposed route connects Granton to the west end and Newhaven to York Place, and a line between Granton and Newhaven to complete the ring. The route is available on the [Edinburgh Local Development Plan ](https://edinburghcouncil.maps.arcgis.com/apps/webappviewer/index.html?id=d1e3d872be424df5b89469de72bb03bd):

![Proposed extension route](https://github.com/robstewart57/edinburgh-trams/raw/master/maps/route-proposal.jpg)

Below I focus on the 5 year plan of extending the line from York Place to Newhaven. In the Scottish government open dataset, there are 1279 *“intermediate geographical zones”*. Below depicts the intermediate zones in close proximity to the proposed extension down Leith Walk and to Newhaven:

| ![Broughton](https://github.com/robstewart57/edinburgh-trams/raw/master/maps/broughton-south.jpg)   Broughton South | ![Broughton](https://github.com/robstewart57/edinburgh-trams/raw/master/maps/easter-road.jpg)   Easter Road and Hawkhill Avenue |
|---|---|
| ![Broughton](https://github.com/robstewart57/edinburgh-trams/raw/master/maps/great-junction-street.jpg)   Great Junction Street | ![Broughton](https://github.com/robstewart57/edinburgh-trams/raw/master/maps/leith-newhaven.jpg)   North Leith and Newhaven |
| ![Broughton](https://github.com/robstewart57/edinburgh-trams/raw/master/maps/pilrig.jpg)   Pilrig | ![Broughton](https://github.com/robstewart57/edinburgh-trams/raw/master/maps/shore.jpg)   The Shore and Constitution Street |
| ![Western Harbour and Leith Docks](https://github.com/robstewart57/edinburgh-trams/raw/master/maps/western-harbour.jpg)   Western Harbour and Leith Docks |  |

### Population growth along the proposed extension

The Scottish government open data portal allows us to query the population growth in each Scottish city, and also within each intermediate zone. Below shows the rate of growth from 2011 to 2015, first at the city level and then at the intermediate zone level.

| ![](https://github.com/robstewart57/edinburgh-trams/raw/master/graphs/national-ratio.png)   National population growth |
|---|
| ![](https://github.com/robstewart57/edinburgh-trams/raw/master/graphs/trams-ratio.png)   Tram extension proximity population growth |

Here are 3 observations about these graphs:

1. The ***population of Edinburgh city is growing faster than Glasgow, Dundee, Stirling and Aberdeen***. Between 2011 and 2015, the population of Edinburgh has grown by 4.4%.
2. The ***population of the intermediate zones in close proximity to the proposed Edinburgh tram extension is growing quickly***. Of the 7 identified zones, the population of 5 zones is growing at a faster rate than the average growth rate across Edinburgh.
3. The ***population of the Western Harbour and Leith Docks zone is growing at a very rapid pace***, where the population grew by 22.7% between 2011 and 2015.

### Reproducing this analysis

These graphs are generated by

1. Running a SPARQL query against the Scottish government dataset service.
2. Plotting graphs from the CSV result set using R.

The SPARQL queries and plotting scripts used for the material in this post are available online at <https://github.com/robstewart57/edinburgh-trams> .

### Summary

This post uses the open Scottish government data to show that the population growth along the proposed tram route extension from York Place to Newhaven is greater than the average for Edinburgh between 2011 and 2015 (zonal growths of up to 23%), a city which itself has the fastest growing population compared to 4 other Scottish cities.

This data validates the 2006 projection that growth in housing demands will increase in the north east of Edinburgh, although measuring any discrepancies in exact numbers is difficult because the 2006 projections were not cross referenced to the intermediate zones that the open dataset uses.

The population data used here is only one of the 17 themes in the Scottish government’s dataset. An extension to this study would explore the other business cases for the tram, namely *economic regeneration and social inclusion* using the other 16 themes, to evaluate the completeness and granularity of economic and societal data at local levels in the Scottish government dataset.