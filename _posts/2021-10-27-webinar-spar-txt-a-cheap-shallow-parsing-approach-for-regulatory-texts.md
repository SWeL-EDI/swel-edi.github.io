---
id: 1283
title: 'Webinar: SPaR.txt &#8211; a cheap Shallow Parsing approach for Regulatory texts'
date: '2021-10-27T11:44:09+01:00'
author: 'Ruben Kruiper'
layout: post
guid: 'https://www.macs.hw.ac.uk/SWeL/?p=1283'
permalink: /2021/10/27/webinar-spar-txt-a-cheap-shallow-parsing-approach-for-regulatory-texts/
categories:
    - Publication
    - Seminar
    - Uncategorized
---

I’ll be presenting my slides for the [NLLP](https://nllpw.org/) (legal NLP) workshop during [EMNLP 2021](https://2021.emnlp.org/). We’ve created a text processing tool that can be used as a building block for ACC (Automated Compliance Checking) using semantic parsing. This work has been done in collaboration with Ioannis Konstas, Alasdair Gray, Farhad Sadeghineko, Richard Watson and Bimal Kumar, and is part of the Intelligent Regulatory Compliance (i-ReC) project, a collaboration between Northumbria University and HWU. You can find our data and code at: <https://github.com/rubenkruiper/SPaR.txt>

**Title:** SPaR.txt – a cheap Shallow Parsing approach for Regulatory texts

**Summary:**  
Understanding written instructions is a notoriously hard task for computers. One can imagine that the task becomes harder when more and more instructions are given at once, especially when these instructions can be ambiguous or even conflicting. These reasons, amongst others, are why it is so hard to achieve (semi-)automated regulatory compliance checking — something that has been researched in the fields of Architecture, Engineering, and Construction (AEC) since the early 80s.   
  
One necessary part of the puzzle is that a computer must recognise entities in a text, e.g., that a `party wall’ is not someone dressed up for halloween but a wall shared by multiple buildings. We’d like a computer to understand such domain-specific terms. But we don’t want to spend a lot of time defining exactly which words and word combinations belong to our domain lexicon. Therefore, we developed a tool that can help us identify groups of words (in the context of a sentence) that are likely a term of interest.

<figure class="wp-block-image">![](https://www.macs.hw.ac.uk/SWeL/wp-content/uploads/2021/10/Screenshot-2021-10-28-at-15.56.44.jpg)<figcaption>Example of the annotation scheme, see Figure 2 in [our preprint](https://arxiv.org/abs/2110.01295).</figcaption></figure>We show that it is easy to train our tool — a simple annotation task, but also few training examples needed to achieve reasonable results. Even using just 200 annotated sentences the tool achieves 70,3% exact matches and 24,2% partial matches for entities. The output of this tool (currently focused on the AEC domain) can be used to improve Information Retrieval results and help assemble a lexicon of terminology in support of semantic parsing.