---
id: 278
title: 'Will the real Kevin Macleod please line up?'
date: '2016-09-09T15:30:35+01:00'
author: 'Alasdair Gray'
excerpt: 'Last week I attended the Digitising Scotland Project&nbsp;Colloquium at Raasay House&nbsp;(featured image above) on the Isle of Raasay. The colloquium was a gathering of historians and computer scientists to discuss the challenges of linking the vital records of the people of Scotland between 1851 and 1974. The Digitising Scotland Project is having the birth, marriage, [&hellip;]'
layout: post
guid: 'http://www.macs.hw.ac.uk/~ajg33/?p=370'
permalink: 'http://www.macs.hw.ac.uk/~ajg33/will-the-real-kevin-macleod-please-line-up/'
enclosure:
    - "\n\n"
syndication_source:
    - 'Alasdair J G Gray'
syndication_source_uri:
    - 'http://www.macs.hw.ac.uk/~ajg33'
syndication_source_id:
    - 'http://www.macs.hw.ac.uk/~ajg33/feed/'
syndication_feed:
    - 'http://www.macs.hw.ac.uk/~ajg33/feed/'
syndication_feed_id:
    - '1'
syndication_permalink:
    - 'http://www.macs.hw.ac.uk/~ajg33/will-the-real-kevin-macleod-please-line-up/'
syndication_item_hash:
    - 4c46d1561f7647633e350e8edfee193e
    - c904bd471c60bf0c0e49085fefaa1e5a
categories:
    - ADRC-Scotland
    - 'Linked Data'
    - Research
---

Last week I attended the [Digitising Scotland Project](http://www.lscs.ac.uk/projects/digitising-scotland/) Colloquium at [Raasay House](https://www.raasay-house.co.uk/) (featured image above) on the Isle of Raasay. The colloquium was a gathering of historians and computer scientists to discuss the challenges of linking the vital records of the people of Scotland between 1851 and 1974.

The Digitising Scotland Project is having the birth, marriage, and death records of Scotland transcribed from the scans of the original hand written registration books. This process is not without its own challenges, try reading [this birth record](http://www.scotlandspeople.gov.uk/content/images/crmbirthjune1868l.jpg) of a famous [Scottish artist and architect](https://en.wikipedia.org/wiki/Charles_Rennie_Mackintosh), but the focus of the colloquium was on what happens after the records have been transcribed.

Each Scottish vital record identifies several individuals, e.g. on a birth record you will have the baby, their parents, the informant, and the registrar. The same individuals will appear on multiple records relating to events in their own life, e.g. an individual will have a birth record, potentially one or more marriage records, and a death record, assuming that they have not emigrated. They can also appear in the records of other individuals, e.g. as a mother on a birth record, the mother-of-the-bride on a marriage record, or the doctor on a death record. The challenge is how to identify the same individual across all the records, when all you have is a name (first and last) and potentially the age.

The problem is compounded in an area like Skye, which was one of the focus regions of the Digitising Scotland project, because there is a relatively small distribution of names on which to draw upon. For example, a name like Kevin Macleod will appear on multiple records. In some cases the name will correspond to a single Kevin Macleod, in other cases it will be a closely related Kevin Macleod, e.g. Kevin Macleod the father of Kevin Macleod, and in others the two Kevin Macleods will not be related at all. The challenge is how to develop a computer algorithm that is capable of making these distinctions.

The colloquium was a great opportunity for historians and computer scientists to discuss the challenges and help each other to develop a solution. However, first we had to agree on a common understanding for terms such as “record” and “individual”.

Overall, we made great progress on exchanging ideas and techniques. We heard how similar challenges are being addressed in a related project focusing on North Orkney, how historians approach the record linkage challenge, and about work for automatically classifying causes of death to their [ICD10](http://www.who.int/classifications/icd/en/) code and jobs to [HISCO](https://socialhistory.org/en/projects/hisco-history-work). There was also time to socialise and enjoy some of the scenery of Raasay, which is a beautiful island the size of Manhattan but with a population of only 160.

<div class="wp-caption alignleft" id="attachment_380" style="width: 310px">[![View from the meeting room](http://www.macs.hw.ac.uk/~ajg33/wp-content/uploads/2016/09/2016-08-28-18.21.26-300x225.jpg)](http://www.macs.hw.ac.uk/~ajg33/wp-content/uploads/2016/09/2016-08-28-18.21.26.jpg)View from the meeting room

</div><div class="wp-caption aligncenter" id="attachment_381" style="width: 310px">[![Sunset over Portree, Skye](http://www.macs.hw.ac.uk/~ajg33/wp-content/uploads/2016/09/2016-08-28-20.55.24-300x225.jpg)](http://www.macs.hw.ac.uk/~ajg33/wp-content/uploads/2016/09/2016-08-28-20.55.24.jpg)Sunset over Portree, Skye

</div>