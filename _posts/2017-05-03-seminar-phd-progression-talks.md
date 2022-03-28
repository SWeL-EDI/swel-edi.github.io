---
id: 508
title: 'Seminar: PhD Progression Talks'
date: '2017-05-03T09:52:24+01:00'
author: 'Alasdair Gray'
layout: post
guid: 'http://www.macs.hw.ac.uk/SWeL/?p=508'
permalink: /2017/05/03/seminar-phd-progression-talks/
categories:
    - ADRC-Scotland
    - Presentation
    - Research
    - Seminar
---

A double bill of PhD progression talks (abstracts below):

- [Ahmad Alsadeeqi: Evaluating Record Linkage Techniques](#Ahmad)
- [Ruben Kruiper: Computer-Aided Biomimetics: Knowledge Extraction](#Ruben)

**Venue:** 3.07 Earl Mountbatten Building, Heriot-Watt University, Edinburgh

**Time and Date:** 11:15, 8 May 2017

## Evaluating Record Linkage Techniques

*Ahmad Alsadeeqi*

Many computer algorithms have been developed to automatically link historical records based on a variety of string matching techniques. These generate an assessment of how likely two records are to be the same. However, it remains unclear how to assess the quality of the linkages computed due to the absence of absolute knowledge of the correct linkage of real historical records – the ground truth. The creation of synthetically generated datasets for which the ground truth linkage is known helps with the assessment of linkage algorithms but the data generated is too clean to be representative of historical records.

We are interested in assessing data linkage algorithms under different data quality scenarios, e.g. with errors typically introduced by a transcription process or where books can be nibbled by mice. We are developing a data corrupting model that injects corruptions into datasets based on given corruption methods and probabilities. We have classified different forms of corruptions found in historical records into four types based on the effect scope of the corruption. Those types are character level (e.g. an f is represented as an s – OCR Corruptions), attribute level (e.g. gender swap – male changed to female due to false entry), record level (e.g. missing records due to different reasons like loss of certificate), and group of records level (e.g. coffee spilt over a page, lost parish records in fire). This will give us the ability to evaluate record linkage algorithms over synthetically generated datasets with known ground truth and with data corruptions matching a given profile.

## Computer-Aided Biomimetics: Knowledge Extraction

*Ruben Kruiper*

Biologically inspired design concerns copying ideas from nature to various other domains, e.g. natural computing. Biomimetics is a sub-field of biologically inspired design and focuses specifically on solving technical/engineering problems. Because engineers lack biological knowledge the process of biomimetics is non-trivial and remains adventitious. Therefore, computational tools have been developed that aim to support engineers during a biomimetics process by integrating large amounts of relevant biological knowledge. Existing tools work apply NLP techniques on biological research papers to build dedicated knowledge bases. However, these existing tools impose an engineering view on biological data. I will talk about the support that ‘Computer-Aided Biomimetics’ tools should provide, introducing a theoretical basis for further research on the appropriate computational techniques.