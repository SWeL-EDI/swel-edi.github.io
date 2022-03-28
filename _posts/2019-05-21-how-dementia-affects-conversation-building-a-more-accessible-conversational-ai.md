---
id: 1064
title: 'How Dementia Affects Conversation: Building a More Accessible Conversational AI'
date: '2019-05-21T15:04:41+01:00'
author: 'Angus Addlesee'
excerpt: '<h4>Diving into the Literature - What do we&nbsp;know?</h4><figure><img alt="" src="https://cdn-images-1.medium.com/max/1024/1*Q7VitMabHpr24zF9R1YztA.jpeg"><figcaption><a href="https://www.whowillyouempower.com/craigsblog/2015/4/13/21-conversation-starters-to-get-your-family-talking">source</a></figcaption></figure><p>We all (roughly) know how to naturally converse with one another. This is mostly subconscious and only really noticeable if an interaction skews from what most consider &ldquo;normal.&rdquo; In the majority of cases, these are just minor differences, such as someone speaking a little too close or interrupting more often than&nbsp;usual.</p><p>However, more significant conversational differences can start to occur when parts of the brain begin to decline in performance.</p><h3>Contents</h3><p><a href="https://medium.com/@addlesee?source=rss-7f06284203ea------2#3e0d">Introduction</a><br><a href="https://medium.com/@addlesee?source=rss-7f06284203ea------2#bfe8">Overview of Dementia</a><br><a href="https://medium.com/@addlesee?source=rss-7f06284203ea------2#d338">Papers Covered</a><br><a href="https://medium.com/@addlesee?source=rss-7f06284203ea------2#6dde">Motivation - Why Speech?</a><br><a href="https://medium.com/@addlesee?source=rss-7f06284203ea------2#9a8c">Datasets</a><br><a href="https://medium.com/@addlesee?source=rss-7f06284203ea------2#0e98">Models</a><br><a href="https://medium.com/@addlesee?source=rss-7f06284203ea------2#bd4c">Important Language Features</a><br><a href="https://medium.com/@addlesee?source=rss-7f06284203ea------2#0a7b">Conclusion</a></p><h3>Introduction</h3><p>I am currently working towards creating a more natural conversational agent (such as Siri, Alexa, etc&hellip;) for those with cognitive impairments that can potentially benefit the most from these systems. Currently we have to adapt how we speak to these systems and have to know exactly how to ask for certain functions. For those that struggle to adapt, I hope to lower some of these barriers so that these people can live more independently for longer. If you want to read more about the overall project then I discussed it in more detail <a href="https://companyconnecting.com/news/conversational-ai-angus-addlesee-heriot-watt">in an interview here</a>.</p><p>To kick off this project with <a href="https://medium.com/wallscope">Wallscope</a> and <a href="https://twitter.com/DataLabScotland">The Data Lab</a>, I first investigated some of the research centered on <a href="https://towardsdatascience.com/beginning-to-replicate-natural-conversation-in-real-time-d4f6b7f62e08?source=friends_link&amp;sk=58b50bb44a3d9ef2d21bd89768284a06">recreating natural conversation with conversational agents</a>. This research all related to a healthy population, but a question arose: do some of these phenomena vary when conversing with those that have forms of cognitive impairment?</p><p>In my previous article, I covered two papers that discuss end-of-turn prediction. They created brilliant models to predict when someone has finished their turn to replace models that just wait for a duration of&nbsp;silence.</p><blockquote>If someone with Dementia takes a little longer to remember the word(s) they&rsquo;re looking for, the silence threshold models used in current systems will interrupt them. I suspect the research models would also perform worse than with a healthy population, so <strong>I&rsquo;m collecting a corpus to investigate this</strong>.</blockquote><p>As my ultimate aim is to make conversational agents more naturally usable for those with dementia, I&rsquo;ll dive into some of the related research in this&nbsp;article.</p><h3>Overview of&nbsp;Dementia</h3><p>I am by no means a dementia expert so this information was all collected from an amazing <a href="https://www.youtube.com/playlist?list=PL6Qsh0P6vDZKyjAyUYidyPk2lLBZCD1ul">series of videos</a> by the Alzheimer&rsquo;s Society.</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/1024/0*hoYXM3ZOUDBhe-kB.jpg"><figcaption><a href="https://www.alzheimers.org.uk/">Their Website</a></figcaption></figure><p>Dementia is not a disease but the name for a group of symptoms that commonly include problems&nbsp;with:</p><ul><li>Memory</li><li>Thinking</li><li>Problem Solving</li><li><strong>Language</strong></li><li>Visual Perception</li></ul><p>For people with dementia, these symptoms have progressed enough to affect daily life and are not a natural part of aging, as they&rsquo;re caused by different diseases (I highlight some of them&nbsp;below).</p><p>All of these diseases cause the loss of nerve cells, and this gets gradually worse over time, as these nerve cells cannot be replaced.</p><p>As more and more cells die, the brain shrinks (atrophies) and symptoms sharpen. Which symptoms set in first depends on which part of the brain atrophies&mdash;so people are impacted differently.</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/1008/0*8P38b8_zopYNxqGF.png"><figcaption><a href="https://www.semanticscholar.org/paper/Progressive-Brain-Atrophy-due-to-Chronic-Alcohol-Slobodin-Odeh/176afa694ce0f92d5be36d3c709ab9dd23dd7e52/figure/0">source</a>&#8202;&mdash;&#8202;you can see the black areas expanding as nerve cells die and atrophy progresses.</figcaption></figure><p>For example, if the occipital lobe begins to decline, then <a href="https://heartbeat.fritz.ai/the-ancient-secrets-of-computer-vision-2-by-joseph-redmon-condensed-934e16eacb44">visual</a> symptoms would progress, whereas losing the temporal lobe would cause language problems&hellip;</p><p>Other common symptoms&nbsp;impact:</p><ul><li>Day-to-day memory</li><li>Concentration</li><li>Organization</li><li>Planning</li><li>Language</li><li>Visual Perception</li><li>Mood</li></ul><blockquote><em>There is currently no&nbsp;cure&hellip;</em></blockquote><p>Before moving on to cover recent research surrounding language problems, it&rsquo;s important to not that most research is disease-specific. Therefore, I&rsquo;lll briefly cover the four types of Dementia.</p><p>All of this information again comes from the <a href="https://www.youtube.com/playlist?list=PL6Qsh0P6vDZKyjAyUYidyPk2lLBZCD1ul">series of videos</a> created by the <a href="https://www.alzheimers.org.uk/">Alzheimer&rsquo;s Society</a>.</p><h4>Alzheimer''s Disease</h4><p>The most common type of dementia is Alzheimer&rsquo;s Disease (AD), and for this reason, it&rsquo;s also the most understood (you&rsquo;ll notice this in the research).</p><p>A healthy brain contains proteins (two of which are called amyloid and tau), but if the brain starts to function abnormally, these proteins form abnormal deposits called plaques and&nbsp;tangles.</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/450/0*fSI5xX9dZ3ITkeql"><figcaption><a href="https://alzscience.wordpress.com/tag/tau/">source</a></figcaption></figure><p>These plaques and tangles damage nerve cells, which causes them to die and the brain to shrink, as shown&nbsp;above.</p><p>The hippocampus is usually the first area of the brain to decline in performance when someone has AD. This is unfortunately where memories are formed, so people will often forget what they have just done and may therefore <strong>repeat themselves in conversation</strong>.</p><p>Recent memories are lost first, whereas childhood memories can still be retrieved as they depend less on the hippocampus. Additionally, emotions can usually be recalled as the amygdala is still intact, whereas the facts surrounding those emotions can be&nbsp;lost.</p><p>AD gradually progresses, so symptoms worsen and become more numerous slowly over&nbsp;time.</p><h4>Vascular Dementia</h4><p>The second most common type of dementia is vascular dementia, which is caused by problems with the brain&rsquo;s blood&nbsp;supply.</p><p>Nerve cells need oxygen and nutrients to survive, so without them they become damaged and die. Therefore, when blood supply is interrupted by a blockage or leak, significant damage can be&nbsp;caused.</p><p>Like with AD, symptoms depend on which parts of the brain are impacted. When the parts damaged are responsible for memory, thinking, or language, the person will have problems remembering, thinking or speaking.</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/400/0*_YEB3AtBqgAZv-Nu.jpg"><figcaption><a href="https://www.alz.org/alzheimers-dementia/what-is-dementia/types-of-dementia/vascular-dementia">source</a></figcaption></figure><p>Vascular dementia can be caused by strokes. Sometimes one major stroke can cause it, but in other cases a person may suffer from multiple smaller strokes that gradually cause&nbsp;damage.</p><p>The most common cause of vascular dementia is small-vessel disease, which gradually narrows the vessels in the brain. As the narrowing continues and spreads, more of the brain gets&nbsp;damaged.</p><p>Vascular dementia can therefore have a gradual progression like AD or, if caused by strokes, a step-like progression with symptoms worsening after each&nbsp;stroke.</p><h4>Dementia with Lewy&nbsp;Bodies</h4><p>Closely related to AD, but less common, is a type of dementia called dementia with Lewy&nbsp;bodies.</p><p>Lewy bodies are tiny clumps of protein that develop inside nerve cells in the brain. This prevents communication between cells, which causes them to&nbsp;die.</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/400/0*q91ZG2nApF5q90JD.jpg"><figcaption><a href="https://www.alz.org/alzheimers-dementia/what-is-dementia/types-of-dementia/lewy-body-dementia">source</a></figcaption></figure><p>Researchers have not yet identified why Lewy bodies form or how. We do know, however, that they can form in any part of the brain, which, again, leads to varying symptoms.</p><p>People can have problems with concentration, movement, alertness, and can even have visual hallucinations. These hallucinations are often distressing and lead to sleep problems.</p><p>Dementia with Lewy bodies progresses gradually and spreads as more nerve cells get damaged, so memory is always impacted eventually.</p><h4>Frontotemporal dementia</h4><p>The last type of dementia I&rsquo;ll cover is frontotemporal dementia (FTD), which is a range of conditions in which cells in the frontal and temporal lobes of the brain are&nbsp;damaged.</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/600/0*ks8ArN3sOpR_eBuC"><figcaption><a href="https://enableme.org.au/Resources/Brain-and-Arteries">source</a></figcaption></figure><p>FTD is again a less common type of dementia but is surprisingly more likely to effect younger people (below&nbsp;65).</p><p>The frontal and temporal lobes of the brain control behavior, emotion, and language, and symptoms occur in the opposite order depending on which lobe is impacted&nbsp;first.</p><p>The frontal lobe is usually the first to decline in performance, so changes begin to show through a person&rsquo;s personality, behavior, and inhibitions.</p><p>Alternatively, when the temporal lobe is impacted first, a person will struggle with language. For example, they may <strong>struggle to find the right&nbsp;word</strong>.</p><p>FTD is thought to occur when proteins such as tau build up in nerve cells, but unlike the other causes, this is likely hereditary.</p><p>Eventually as FTD progresses, symptoms of frontal and temporal damage overlap, and both&nbsp;occur.</p><h3>Papers Covered</h3><p>That overview of dementia was fairly in depth, so we should now have a common foundation for this article and all subsequent articles.</p><p>As we now know, difficulty with language is a common symptom of dementia, so in order to understand how it changes, I&rsquo;ll cover four papers that investigate this. These include the following:</p><p>[1]</p><blockquote><strong>A Speech Recognition Tool for Early Detection of Alzheimer&rsquo;s Disease </strong>by Brianna Marlene Broderick, Si Long Tou and Emily Mower&nbsp;Provost</blockquote><p>[2]</p><blockquote><strong>A Method for Analysis of Patient Speech in Dialogue for Dementia Detection</strong> by Saturnino Luz, Sofia de la Fuente and Pierre&nbsp;Albert</blockquote><p>[3]</p><blockquote><strong>Speech Processing for Early Alzheimer Disease Diagnosis: Machine Learning Based Approach </strong>by Randa Ban Ammar and Yassine Ben&nbsp;Ayed</blockquote><p>[4]</p><blockquote><strong>Detecting Cognitive Impairments by Agreeing on Interpretations of Linguistic Features </strong>by Zining Zhu, Jekaterina Novikova and Frank&nbsp;Rudzicz</blockquote><blockquote>Note: I will refer to each paper with their corresponding number from now&nbsp;on.</blockquote><h3>Motivation - Why&nbsp;Speech?</h3><p>These four papers have a common motivation: to detect dementia in a more cost-effective and less intrusive manner.</p><p>These papers tend to focus on Alzheimer&rsquo;s Disease (AD) because, as [3] mentions, 60&ndash;80% of dementia cases are caused by AD. I would add that this is likely why AD features most in existing datasets, also.</p><h4>Current Detection Methods</h4><p>[1] points out that dementia is relatively difficult to diagnose as progression and symptoms vary widely. The diagnostic processes are therefore complex, and dementia often goes undiagnosed because of&nbsp;this.</p><p>[2] explains that imaging (such as PET or MRI scans) and cerebrospinal fluid analysis can be used to detect AD very accurately, but these methods are expensive and extremely invasive. A lumbar puncture must be performed to collect cerebrospinal fluid, for&nbsp;example.</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/320/0*Vl8bPVc_uNsVpmi1.jpg"><figcaption><a href="https://www.nhs.uk/conditions/lumbar-puncture/">source</a> - lumbar puncture aka &ldquo;spinal&nbsp;tap&rdquo;</figcaption></figure><p>[2] also points out that neuropsychological detection methods have been developed that can, to varying levels of accuracy, detect signs of AD. [1] adds that these often require repeat testing and are therefore time-consuming and cause additional stress and confusion to the&nbsp;patient.</p><p>As mentioned above, [1] argues that dementia often goes undiagnosed because of these flaws. [2] agrees that it would be beneficial to detect AD pathology long before someone is actually diagnosed in order to implement secondary prevention.</p><h4>Will Speech Analysis&nbsp;Help?</h4><p>As repeatedly mentioned in the overview of dementia above, language is known to be impacted through various signs such as struggles with word-finding, understanding difficulties, and repetition. [3] points out that language relies heavily on memory, and for this reason, one of the earliest signs of AD may be in a person&rsquo;s&nbsp;speech.</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/445/0*x7ReNU_bZR13CCqq.jpeg"><figcaption><a href="https://www.daianastoicescu.com/2019/04/do-you-have-awareness-in-conversation/">source</a></figcaption></figure><p>[2] reinforces this point by highlighting the fact that in order to communicate successfully, a person must be able to perform complex decision making, strategy planning, consequence foresight, and problem solving. These are all impaired as dementia progresses.</p><p>Practically, [2] states that speech is easy to acquire and elicit, so they (along with [1], [3], and [4]) propose that speech could be used to diagnose Dementia in a cost-effective, non-invasive, and timely&nbsp;manner.</p><p>To start investigating this, we need the&nbsp;data.</p><h3>Datasets</h3><p>As you can imagine, it isn&rsquo;t easy to acquire suitable datasets to investigate this. For this reason [1], [3], and [4] used the same dataset from <a href="https://dementia.talkbank.org/">DementiaBank</a> (a repository within <a href="https://talkbank.org/">TalkBank</a>) called the Pitt Corpus. This corpus contains audio and transcriptions of people with AD and healthy elderly controls.</p><p>To elicit speech, participants (both groups) were asked to describe the Cookie Theft stimulus&nbsp;photo:</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/749/0*tBRhdfbvwJCKjny0.png"><figcaption><a href="https://languagelog.ldc.upenn.edu/nll/?p=40027">source</a></figcaption></figure><p>Some participants had multiple visits, so [1], [3], and [4] had audio and transcriptions for 223 control interviews and 234 AD interviews (these numbers differ slightly between them due to pre-processing, I&nbsp;expect).</p><p>[1] points out that the picture description task ensures the vocabulary and speech elicited is controlled around a context, but [2] wanted to investigate a different type of&nbsp;speech.</p><p>Instead of narrative or picture description speech, [2] used spontaneous conversational data from the Carolina <a href="https://carolinaconversations.musc.edu/about/">Conversations Collection</a> (CCC) to create their&nbsp;models.</p><p>The corpus contains 21 interviews with patients with AD and 17 dialogues with control patients. These control patients suffered from other conditions such as diabetes, heart problems, etc&hellip; None of them had any neuropsychological conditions, however.</p><p>The automatic detection of AD developed by [2] was the first use of low-level dialogue interaction data as a basis for AD detection on spontaneous spoken language.</p><h3>Models</h3><p>If I&rsquo;m to build a <a href="https://towardsdatascience.com/beginning-to-replicate-natural-conversation-in-real-time-d4f6b7f62e08?source=friends_link&amp;sk=58b50bb44a3d9ef2d21bd89768284a06">more natural conversational system</a>, then I must be aware of the noticeable differences in speech between those with dementia and healthy controls. What features inform the models in these papers the most should indicate exactly&nbsp;that.</p><p>[1] extracted features that are known to be impacted by AD (I run through the exact features in the next section, as that&rsquo;s my primary interest). They collected many transcription-based features and acoustic features before using principal component analysis (PCA) to reduce the total number of features to train with. Using the selected features they trained a KNN &amp; SVM to achieve an F1 of 0.73 and importantly, a recall of 0.83 as false negatives could be dangerous.</p><p>[2] decided to only rely on content-free features including speech rate, turn-taking patterns, and other parameters. They found that when they used speech rate and turn-taking patterns to train a Real AdaBoost algorithm, they achieved an accuracy of 86.5%, and adding more features reduced the number of false positives. They found that other models performed comparably well, but even though Real AdaDoost and <a href="https://heartbeat.fritz.ai/introduction-to-decision-tree-learning-cd604f85e236">decision trees</a> achieved an accuracy of 86.5%, they say there&rsquo;s still room for improvement.</p><p>One point to highlight about [2] is their high accuracy (comparable to the state-of-the-art) despite relying only on content-free features. Their model can therefore be used globally, as the features are not language-dependent like the more complex lexical, syntactic, and semantic features used by other&nbsp;models.</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/960/0*0X7fw7j95JBI8qzF.jpg"><figcaption><a href="https://pixabay.com/illustrations/earth-globalisation-network-3866609/">source</a></figcaption></figure><p>[3] ran feature extraction, feature selection, and then classification. There were many syntactic, semantic, and pragmatic features transcribed in the corpus. They tried three feature selection methods, namely: Information Gain, KNN, and SVM Recursive Feature Elimination. This feature selection step is particularly interesting for my project. Using the features selected by the KNN, their most accurate model was an SVM that achieved precision of&nbsp;79%.</p><blockquote>[4] introduces a completely different (and more interesting) approach than the other papers, as they build a Consensus Network&nbsp;(CN).</blockquote><p>As [4] uses the same corpus as [1] and [3], there&rsquo;s a point at which the only two ways to improve upon previous classifiers are to either add more data or calculate more features. Of course, both of those options have limits, so this is why [4] takes a novel approach.</p><p>They first split the extracted features into non-overlapping subsets and found that the three naturally occurring groups (acoustic, syntactic, and semantic) garnered the best&nbsp;results.</p><p>The 185 acoustic features, 117 syntactic features, and 31 semantic features (plus 80 POS features that were mainly semantic) were used to train three separate neural networks called &ldquo;ePhysicians&rdquo;:</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/574/1*zdcwSghJfCZXkRNvFs-LKg.png"><figcaption>[4]</figcaption></figure><p>Each ePhysician is a fully connected network with ten hidden layers, Leaky ReLU activations, and batch normalization. Both the classifier and discriminator were the same but without any hidden&nbsp;layers.</p><p>The output of each ePhysician was passed one-by-one into the discriminator (with noise), and it then tried to to tell the ePhysicians apart. This encourages the ePhysicians to output indistinguishable representations from each other&nbsp;(agree).</p><p>[4] indeed found that their CN, with the three naturally occurring and non-overlapping subsets of features, outperformed other models with a macro F1 of 0.7998. Additionally, [4] showed that the inclusion of noise and cooperative optimization did contribute to the performance.</p><blockquote>In case of confusion, it&rsquo;s important to reiterate that [2] used a different corpus.</blockquote><p>Each paper, especially [4], describes their model in more detail, of course. I&rsquo;m not primarily interested in the models themselves, as I don&rsquo;t intend to diagnose dementia. My main focus in this article is to find out which features were used to train these models, as I&rsquo;ll have to pay attention to the same features.</p><h3>Important Language&nbsp;Features</h3><p>In order for a conversational system to <a href="https://towardsdatascience.com/beginning-to-replicate-natural-conversation-in-real-time-d4f6b7f62e08?source=friends_link&amp;sk=58b50bb44a3d9ef2d21bd89768284a06">perform more naturally</a> for those with cognitive impairments, how language changes must be investigated.</p><p>[4] sent all features to their ePhysicians so didn&rsquo;t detail which features were most predictive. They did mention that pronoun-noun ratios were known to change, as those with cognitive impairments use more pronouns than&nbsp;nouns.</p><p>[2] interestingly achieved great results using just a person&rsquo;s speech rate and turn-taking patterns. They did obtain less false positives by adding other features but stuck to content-free features, as mentioned. This means that their model does not depend on a specific language and can therefore be used on a global&nbsp;scale.</p><p>[1] extracted features that are known to be impacted by AD and additionally noted that patients&rsquo; vocabulary and semantic processing had declined.</p><p>[1] listed the following <strong>transcription-based features</strong>:</p><ul><li>Lexical Richness</li><li>Utterance Length</li><li>Frequency of Filler&nbsp;Words</li><li>Frequency of&nbsp;Pronouns</li><li>Frequency of&nbsp;Verbs</li><li>Frequency of Adjectives</li><li>Frequency of Proper&nbsp;Nouns</li></ul><p>and [1] listed the following <strong>acoustic features</strong>:</p><ul><li>Word Finding&nbsp;Errors</li><li>Fluidity</li><li>Rhythm of&nbsp;Speech</li><li>Pause Frequency</li><li>Duration</li><li>Speech Rate</li><li>Articulation Rate</li></ul><p>Brilliantly, [3] performed several feature selection methods upon the following features:</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/530/1*tcBzqoHyxbOijm9y0FW0pA.png"><figcaption>[3]</figcaption></figure><p>Upon all of these features, they implemented three feature selection methods to select the top eight features each: Information Gain, KNN, and SVM Recursive Feature Elimination (SVM-RFE).</p><p>They output the following:</p><figure><img alt="" src="https://cdn-images-1.medium.com/max/550/1*YL7QNYixLY4mmdiXReFRJQ.png"><figcaption>[3]</figcaption></figure><p>Three features were selected by all three methods, suggesting that they&rsquo;re highly predictive for detecting AD: Word Errors, Number of Prepositions, and Number of Repetitions.</p><p>It&rsquo;s also important to restate that the most accurate model used the features selected by the KNN&nbsp;method.</p><p>Overall, we have many features identified in this section to pay attention to. In particular, however, (from both the four papers and the Alzheimer&rsquo;s Society videos) we need to pay particular attention to:</p><ul><li>Word Errors</li><li>Repetition</li><li>Pronoun-Noun Ratio</li><li>Number of Prepositions</li><li>Speech Rate</li><li>Pause Frequency</li></ul><h3>Conclusion</h3><p>We&rsquo;ve previously looked into the current research towards <a href="https://towardsdatascience.com/beginning-to-replicate-natural-conversation-in-real-time-d4f6b7f62e08?source=friends_link&amp;sk=58b50bb44a3d9ef2d21bd89768284a06">making conversational systems more natural</a>, and we now have a relatively short list of features that must be handled if conversational systems are to perform fluidly, even if the user has a cognitive impairment like&nbsp;AD.</p><p>Of course, this isn&rsquo;t an exhaustive list, but it&rsquo;s a good place to start and points me in the right direction for what to work on next. Stay&nbsp;tuned!</p><p><em>Editor&rsquo;s Note:</em><a href="http://bit.ly/heartbeatslack"><em> Join Heartbeat on Slack</em></a><em> and follow us on</em><a href="https://twitter.com/fritzlabs"><em> Twitter</em></a><em> and</em><a href="https://www.linkedin.com/company/fritz-labs-inc/"><em> LinkedIn</em></a><em> for the all the latest content, news, and more in machine learning, mobile development, and where the two intersect.</em></p><a href="https://medium.com/media/05616eaceabf5537ffbda5b6811c367c/href">https://medium.com/media/05616eaceabf5537ffbda5b6811c367c/href</a><img src="https://medium.com/_/stat?event=post.clientViewed&amp;referrerSource=full_rss&amp;postId=f538d2d9507a" width="1" height="1"><hr><p><a href="https://heartbeat.fritz.ai/how-dementia-effects-conversation-f538d2d9507a">How Dementia Affects Conversation: Building a More Accessible Conversational AI</a> was originally published in <a href="https://heartbeat.fritz.ai/">Heartbeat</a> on Medium, where people are continuing the conversation by highlighting and responding to this story.</p>'
layout: post
guid: 'https://medium.com/p/f538d2d9507a'
permalink: 'https://heartbeat.fritz.ai/how-dementia-effects-conversation-f538d2d9507a?source=rss-7f06284203ea------2'
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
    - 'https://heartbeat.fritz.ai/how-dementia-effects-conversation-f538d2d9507a?source=rss-7f06284203ea------2'
syndication_item_hash:
    - d20973bd4099e5836c4dc7d26541c9d7
    - cf2469055f44dce8737ff2886df67cd2
    - cf2469055f44dce8737ff2886df67cd2
    - 4f404bf516c89e45e9ea2f8e2936d8b6
categories:
    - ai
    - heartbeat
    - machine-learning
    - machine-learning-tools
    - speech
---

#### Diving into the Literature - What do we know?

<figure>![](https://cdn-images-1.medium.com/max/1024/1*Q7VitMabHpr24zF9R1YztA.jpeg)<figcaption>[source](https://www.whowillyouempower.com/craigsblog/2015/4/13/21-conversation-starters-to-get-your-family-talking)</figcaption></figure>We all (roughly) know how to naturally converse with one another. This is mostly subconscious and only really noticeable if an interaction skews from what most consider “normal.” In the majority of cases, these are just minor differences, such as someone speaking a little too close or interrupting more often than usual.

However, more significant conversational differences can start to occur when parts of the brain begin to decline in performance.

### Contents

[Introduction](https://heartbeat.fritz.ai/how-dementia-effects-conversation-f538d2d9507a?source=rss-7f06284203ea------2#3e0d)  
[Overview of Dementia](https://heartbeat.fritz.ai/how-dementia-effects-conversation-f538d2d9507a?source=rss-7f06284203ea------2#bfe8)  
[Papers Covered](https://heartbeat.fritz.ai/how-dementia-effects-conversation-f538d2d9507a?source=rss-7f06284203ea------2#d338)  
[Motivation - Why Speech?](https://heartbeat.fritz.ai/how-dementia-effects-conversation-f538d2d9507a?source=rss-7f06284203ea------2#6dde)  
[Datasets](https://heartbeat.fritz.ai/how-dementia-effects-conversation-f538d2d9507a?source=rss-7f06284203ea------2#9a8c)  
[Models](https://heartbeat.fritz.ai/how-dementia-effects-conversation-f538d2d9507a?source=rss-7f06284203ea------2#0e98)  
[Important Language Features](https://heartbeat.fritz.ai/how-dementia-effects-conversation-f538d2d9507a?source=rss-7f06284203ea------2#bd4c)  
[Conclusion](https://heartbeat.fritz.ai/how-dementia-effects-conversation-f538d2d9507a?source=rss-7f06284203ea------2#0a7b)

### Introduction

I am currently working towards creating a more natural conversational agent (such as Siri, Alexa, etc…) for those with cognitive impairments that can potentially benefit the most from these systems. Currently we have to adapt how we speak to these systems and have to know exactly how to ask for certain functions. For those that struggle to adapt, I hope to lower some of these barriers so that these people can live more independently for longer. If you want to read more about the overall project then I discussed it in more detail [in an interview here](https://companyconnecting.com/news/conversational-ai-angus-addlesee-heriot-watt).

To kick off this project with [Wallscope](https://medium.com/wallscope) and [The Data Lab](https://twitter.com/DataLabScotland), I first investigated some of the research centered on [recreating natural conversation with conversational agents](https://towardsdatascience.com/beginning-to-replicate-natural-conversation-in-real-time-d4f6b7f62e08?source=friends_link&sk=58b50bb44a3d9ef2d21bd89768284a06). This research all related to a healthy population, but a question arose: do some of these phenomena vary when conversing with those that have forms of cognitive impairment?

In my previous article, I covered two papers that discuss end-of-turn prediction. They created brilliant models to predict when someone has finished their turn to replace models that just wait for a duration of silence.

> If someone with Dementia takes a little longer to remember the word(s) they’re looking for, the silence threshold models used in current systems will interrupt them. I suspect the research models would also perform worse than with a healthy population, so **I’m collecting a corpus to investigate this**.

As my ultimate aim is to make conversational agents more naturally usable for those with dementia, I’ll dive into some of the related research in this article.

### Overview of Dementia

I am by no means a dementia expert so this information was all collected from an amazing [series of videos](https://www.youtube.com/playlist?list=PL6Qsh0P6vDZKyjAyUYidyPk2lLBZCD1ul) by the Alzheimer’s Society.

<figure>![](https://cdn-images-1.medium.com/max/1024/0*hoYXM3ZOUDBhe-kB.jpg)<figcaption>[Their Website](https://www.alzheimers.org.uk/)</figcaption></figure>Dementia is not a disease but the name for a group of symptoms that commonly include problems with:

- Memory
- Thinking
- Problem Solving
- **Language**
- Visual Perception

For people with dementia, these symptoms have progressed enough to affect daily life and are not a natural part of aging, as they’re caused by different diseases (I highlight some of them below).

All of these diseases cause the loss of nerve cells, and this gets gradually worse over time, as these nerve cells cannot be replaced.

As more and more cells die, the brain shrinks (atrophies) and symptoms sharpen. Which symptoms set in first depends on which part of the brain atrophies—so people are impacted differently.

<figure>![](https://cdn-images-1.medium.com/max/1008/0*8P38b8_zopYNxqGF.png)<figcaption>[source](https://www.semanticscholar.org/paper/Progressive-Brain-Atrophy-due-to-Chronic-Alcohol-Slobodin-Odeh/176afa694ce0f92d5be36d3c709ab9dd23dd7e52/figure/0) — you can see the black areas expanding as nerve cells die and atrophy progresses.</figcaption></figure>For example, if the occipital lobe begins to decline, then [visual](https://heartbeat.fritz.ai/the-ancient-secrets-of-computer-vision-2-by-joseph-redmon-condensed-934e16eacb44) symptoms would progress, whereas losing the temporal lobe would cause language problems…

Other common symptoms impact:

- Day-to-day memory
- Concentration
- Organization
- Planning
- Language
- Visual Perception
- Mood

> *There is currently no cure…*

Before moving on to cover recent research surrounding language problems, it’s important to not that most research is disease-specific. Therefore, I’lll briefly cover the four types of Dementia.

All of this information again comes from the [series of videos](https://www.youtube.com/playlist?list=PL6Qsh0P6vDZKyjAyUYidyPk2lLBZCD1ul) created by the [Alzheimer’s Society](https://www.alzheimers.org.uk/).

#### Alzheimer's Disease

The most common type of dementia is Alzheimer’s Disease (AD), and for this reason, it’s also the most understood (you’ll notice this in the research).

A healthy brain contains proteins (two of which are called amyloid and tau), but if the brain starts to function abnormally, these proteins form abnormal deposits called plaques and tangles.

<figure>![](https://cdn-images-1.medium.com/max/450/0*fSI5xX9dZ3ITkeql)<figcaption>[source](https://alzscience.wordpress.com/tag/tau/)</figcaption></figure>These plaques and tangles damage nerve cells, which causes them to die and the brain to shrink, as shown above.

The hippocampus is usually the first area of the brain to decline in performance when someone has AD. This is unfortunately where memories are formed, so people will often forget what they have just done and may therefore **repeat themselves in conversation**.

Recent memories are lost first, whereas childhood memories can still be retrieved as they depend less on the hippocampus. Additionally, emotions can usually be recalled as the amygdala is still intact, whereas the facts surrounding those emotions can be lost.

AD gradually progresses, so symptoms worsen and become more numerous slowly over time.

#### Vascular Dementia

The second most common type of dementia is vascular dementia, which is caused by problems with the brain’s blood supply.

Nerve cells need oxygen and nutrients to survive, so without them they become damaged and die. Therefore, when blood supply is interrupted by a blockage or leak, significant damage can be caused.

Like with AD, symptoms depend on which parts of the brain are impacted. When the parts damaged are responsible for memory, thinking, or language, the person will have problems remembering, thinking or speaking.

<figure>![](https://cdn-images-1.medium.com/max/400/0*_YEB3AtBqgAZv-Nu.jpg)<figcaption>[source](https://www.alz.org/alzheimers-dementia/what-is-dementia/types-of-dementia/vascular-dementia)</figcaption></figure>Vascular dementia can be caused by strokes. Sometimes one major stroke can cause it, but in other cases a person may suffer from multiple smaller strokes that gradually cause damage.

The most common cause of vascular dementia is small-vessel disease, which gradually narrows the vessels in the brain. As the narrowing continues and spreads, more of the brain gets damaged.

Vascular dementia can therefore have a gradual progression like AD or, if caused by strokes, a step-like progression with symptoms worsening after each stroke.

#### Dementia with Lewy Bodies

Closely related to AD, but less common, is a type of dementia called dementia with Lewy bodies.

Lewy bodies are tiny clumps of protein that develop inside nerve cells in the brain. This prevents communication between cells, which causes them to die.

<figure>![](https://cdn-images-1.medium.com/max/400/0*q91ZG2nApF5q90JD.jpg)<figcaption>[source](https://www.alz.org/alzheimers-dementia/what-is-dementia/types-of-dementia/lewy-body-dementia)</figcaption></figure>Researchers have not yet identified why Lewy bodies form or how. We do know, however, that they can form in any part of the brain, which, again, leads to varying symptoms.

People can have problems with concentration, movement, alertness, and can even have visual hallucinations. These hallucinations are often distressing and lead to sleep problems.

Dementia with Lewy bodies progresses gradually and spreads as more nerve cells get damaged, so memory is always impacted eventually.

#### Frontotemporal dementia

The last type of dementia I’ll cover is frontotemporal dementia (FTD), which is a range of conditions in which cells in the frontal and temporal lobes of the brain are damaged.

<figure>![](https://cdn-images-1.medium.com/max/600/0*ks8ArN3sOpR_eBuC)<figcaption>[source](https://enableme.org.au/Resources/Brain-and-Arteries)</figcaption></figure>FTD is again a less common type of dementia but is surprisingly more likely to effect younger people (below 65).

The frontal and temporal lobes of the brain control behavior, emotion, and language, and symptoms occur in the opposite order depending on which lobe is impacted first.

The frontal lobe is usually the first to decline in performance, so changes begin to show through a person’s personality, behavior, and inhibitions.

Alternatively, when the temporal lobe is impacted first, a person will struggle with language. For example, they may **struggle to find the right word**.

FTD is thought to occur when proteins such as tau build up in nerve cells, but unlike the other causes, this is likely hereditary.

Eventually as FTD progresses, symptoms of frontal and temporal damage overlap, and both occur.

### Papers Covered

That overview of dementia was fairly in depth, so we should now have a common foundation for this article and all subsequent articles.

As we now know, difficulty with language is a common symptom of dementia, so in order to understand how it changes, I’ll cover four papers that investigate this. These include the following:

\[1\]

> **A Speech Recognition Tool for Early Detection of Alzheimer’s Disease** by Brianna Marlene Broderick, Si Long Tou and Emily Mower Provost

\[2\]

> **A Method for Analysis of Patient Speech in Dialogue for Dementia Detection** by Saturnino Luz, Sofia de la Fuente and Pierre Albert

\[3\]

> **Speech Processing for Early Alzheimer Disease Diagnosis: Machine Learning Based Approach** by Randa Ban Ammar and Yassine Ben Ayed

\[4\]

> **Detecting Cognitive Impairments by Agreeing on Interpretations of Linguistic Features** by Zining Zhu, Jekaterina Novikova and Frank Rudzicz

> Note: I will refer to each paper with their corresponding number from now on.

### Motivation - Why Speech?

These four papers have a common motivation: to detect dementia in a more cost-effective and less intrusive manner.

These papers tend to focus on Alzheimer’s Disease (AD) because, as \[3\] mentions, 60–80% of dementia cases are caused by AD. I would add that this is likely why AD features most in existing datasets, also.

#### Current Detection Methods

\[1\] points out that dementia is relatively difficult to diagnose as progression and symptoms vary widely. The diagnostic processes are therefore complex, and dementia often goes undiagnosed because of this.

\[2\] explains that imaging (such as PET or MRI scans) and cerebrospinal fluid analysis can be used to detect AD very accurately, but these methods are expensive and extremely invasive. A lumbar puncture must be performed to collect cerebrospinal fluid, for example.

<figure>![](https://cdn-images-1.medium.com/max/320/0*Vl8bPVc_uNsVpmi1.jpg)<figcaption>[source](https://www.nhs.uk/conditions/lumbar-puncture/) - lumbar puncture aka “spinal tap”</figcaption></figure>\[2\] also points out that neuropsychological detection methods have been developed that can, to varying levels of accuracy, detect signs of AD. \[1\] adds that these often require repeat testing and are therefore time-consuming and cause additional stress and confusion to the patient.

As mentioned above, \[1\] argues that dementia often goes undiagnosed because of these flaws. \[2\] agrees that it would be beneficial to detect AD pathology long before someone is actually diagnosed in order to implement secondary prevention.

#### Will Speech Analysis Help?

As repeatedly mentioned in the overview of dementia above, language is known to be impacted through various signs such as struggles with word-finding, understanding difficulties, and repetition. \[3\] points out that language relies heavily on memory, and for this reason, one of the earliest signs of AD may be in a person’s speech.

<figure>![](https://cdn-images-1.medium.com/max/445/0*x7ReNU_bZR13CCqq.jpeg)<figcaption>[source](https://www.daianastoicescu.com/2019/04/do-you-have-awareness-in-conversation/)</figcaption></figure>\[2\] reinforces this point by highlighting the fact that in order to communicate successfully, a person must be able to perform complex decision making, strategy planning, consequence foresight, and problem solving. These are all impaired as dementia progresses.

Practically, \[2\] states that speech is easy to acquire and elicit, so they (along with \[1\], \[3\], and \[4\]) propose that speech could be used to diagnose Dementia in a cost-effective, non-invasive, and timely manner.

To start investigating this, we need the data.

### Datasets

As you can imagine, it isn’t easy to acquire suitable datasets to investigate this. For this reason \[1\], \[3\], and \[4\] used the same dataset from [DementiaBank](https://dementia.talkbank.org/) (a repository within [TalkBank](https://talkbank.org/)) called the Pitt Corpus. This corpus contains audio and transcriptions of people with AD and healthy elderly controls.

To elicit speech, participants (both groups) were asked to describe the Cookie Theft stimulus photo:

<figure>![](https://cdn-images-1.medium.com/max/749/0*tBRhdfbvwJCKjny0.png)<figcaption>[source](https://languagelog.ldc.upenn.edu/nll/?p=40027)</figcaption></figure>Some participants had multiple visits, so \[1\], \[3\], and \[4\] had audio and transcriptions for 223 control interviews and 234 AD interviews (these numbers differ slightly between them due to pre-processing, I expect).

\[1\] points out that the picture description task ensures the vocabulary and speech elicited is controlled around a context, but \[2\] wanted to investigate a different type of speech.

Instead of narrative or picture description speech, \[2\] used spontaneous conversational data from the Carolina [Conversations Collection](https://carolinaconversations.musc.edu/about/) (CCC) to create their models.

The corpus contains 21 interviews with patients with AD and 17 dialogues with control patients. These control patients suffered from other conditions such as diabetes, heart problems, etc… None of them had any neuropsychological conditions, however.

The automatic detection of AD developed by \[2\] was the first use of low-level dialogue interaction data as a basis for AD detection on spontaneous spoken language.

### Models

If I’m to build a [more natural conversational system](https://towardsdatascience.com/beginning-to-replicate-natural-conversation-in-real-time-d4f6b7f62e08?source=friends_link&sk=58b50bb44a3d9ef2d21bd89768284a06), then I must be aware of the noticeable differences in speech between those with dementia and healthy controls. What features inform the models in these papers the most should indicate exactly that.

\[1\] extracted features that are known to be impacted by AD (I run through the exact features in the next section, as that’s my primary interest). They collected many transcription-based features and acoustic features before using principal component analysis (PCA) to reduce the total number of features to train with. Using the selected features they trained a KNN &amp; SVM to achieve an F1 of 0.73 and importantly, a recall of 0.83 as false negatives could be dangerous.

\[2\] decided to only rely on content-free features including speech rate, turn-taking patterns, and other parameters. They found that when they used speech rate and turn-taking patterns to train a Real AdaBoost algorithm, they achieved an accuracy of 86.5%, and adding more features reduced the number of false positives. They found that other models performed comparably well, but even though Real AdaDoost and [decision trees](https://heartbeat.fritz.ai/introduction-to-decision-tree-learning-cd604f85e236) achieved an accuracy of 86.5%, they say there’s still room for improvement.

One point to highlight about \[2\] is their high accuracy (comparable to the state-of-the-art) despite relying only on content-free features. Their model can therefore be used globally, as the features are not language-dependent like the more complex lexical, syntactic, and semantic features used by other models.

<figure>![](https://cdn-images-1.medium.com/max/960/0*0X7fw7j95JBI8qzF.jpg)<figcaption>[source](https://pixabay.com/illustrations/earth-globalisation-network-3866609/)</figcaption></figure>\[3\] ran feature extraction, feature selection, and then classification. There were many syntactic, semantic, and pragmatic features transcribed in the corpus. They tried three feature selection methods, namely: Information Gain, KNN, and SVM Recursive Feature Elimination. This feature selection step is particularly interesting for my project. Using the features selected by the KNN, their most accurate model was an SVM that achieved precision of 79%.

> \[4\] introduces a completely different (and more interesting) approach than the other papers, as they build a Consensus Network (CN).

As \[4\] uses the same corpus as \[1\] and \[3\], there’s a point at which the only two ways to improve upon previous classifiers are to either add more data or calculate more features. Of course, both of those options have limits, so this is why \[4\] takes a novel approach.

They first split the extracted features into non-overlapping subsets and found that the three naturally occurring groups (acoustic, syntactic, and semantic) garnered the best results.

The 185 acoustic features, 117 syntactic features, and 31 semantic features (plus 80 POS features that were mainly semantic) were used to train three separate neural networks called “ePhysicians”:

<figure>![](https://cdn-images-1.medium.com/max/574/1*zdcwSghJfCZXkRNvFs-LKg.png)<figcaption>\[4\]</figcaption></figure>Each ePhysician is a fully connected network with ten hidden layers, Leaky ReLU activations, and batch normalization. Both the classifier and discriminator were the same but without any hidden layers.

The output of each ePhysician was passed one-by-one into the discriminator (with noise), and it then tried to to tell the ePhysicians apart. This encourages the ePhysicians to output indistinguishable representations from each other (agree).

\[4\] indeed found that their CN, with the three naturally occurring and non-overlapping subsets of features, outperformed other models with a macro F1 of 0.7998. Additionally, \[4\] showed that the inclusion of noise and cooperative optimization did contribute to the performance.

> In case of confusion, it’s important to reiterate that \[2\] used a different corpus.

Each paper, especially \[4\], describes their model in more detail, of course. I’m not primarily interested in the models themselves, as I don’t intend to diagnose dementia. My main focus in this article is to find out which features were used to train these models, as I’ll have to pay attention to the same features.

### Important Language Features

In order for a conversational system to [perform more naturally](https://towardsdatascience.com/beginning-to-replicate-natural-conversation-in-real-time-d4f6b7f62e08?source=friends_link&sk=58b50bb44a3d9ef2d21bd89768284a06) for those with cognitive impairments, how language changes must be investigated.

\[4\] sent all features to their ePhysicians so didn’t detail which features were most predictive. They did mention that pronoun-noun ratios were known to change, as those with cognitive impairments use more pronouns than nouns.

\[2\] interestingly achieved great results using just a person’s speech rate and turn-taking patterns. They did obtain less false positives by adding other features but stuck to content-free features, as mentioned. This means that their model does not depend on a specific language and can therefore be used on a global scale.

\[1\] extracted features that are known to be impacted by AD and additionally noted that patients’ vocabulary and semantic processing had declined.

\[1\] listed the following **transcription-based features**:

- Lexical Richness
- Utterance Length
- Frequency of Filler Words
- Frequency of Pronouns
- Frequency of Verbs
- Frequency of Adjectives
- Frequency of Proper Nouns

and \[1\] listed the following **acoustic features**:

- Word Finding Errors
- Fluidity
- Rhythm of Speech
- Pause Frequency
- Duration
- Speech Rate
- Articulation Rate

Brilliantly, \[3\] performed several feature selection methods upon the following features:

<figure>![](https://cdn-images-1.medium.com/max/530/1*tcBzqoHyxbOijm9y0FW0pA.png)<figcaption>\[3\]</figcaption></figure>Upon all of these features, they implemented three feature selection methods to select the top eight features each: Information Gain, KNN, and SVM Recursive Feature Elimination (SVM-RFE).

They output the following:

<figure>![](https://cdn-images-1.medium.com/max/550/1*YL7QNYixLY4mmdiXReFRJQ.png)<figcaption>\[3\]</figcaption></figure>Three features were selected by all three methods, suggesting that they’re highly predictive for detecting AD: Word Errors, Number of Prepositions, and Number of Repetitions.

It’s also important to restate that the most accurate model used the features selected by the KNN method.

Overall, we have many features identified in this section to pay attention to. In particular, however, (from both the four papers and the Alzheimer’s Society videos) we need to pay particular attention to:

- Word Errors
- Repetition
- Pronoun-Noun Ratio
- Number of Prepositions
- Speech Rate
- Pause Frequency

### Conclusion

We’ve previously looked into the current research towards [making conversational systems more natural](https://towardsdatascience.com/beginning-to-replicate-natural-conversation-in-real-time-d4f6b7f62e08?source=friends_link&sk=58b50bb44a3d9ef2d21bd89768284a06), and we now have a relatively short list of features that must be handled if conversational systems are to perform fluidly, even if the user has a cognitive impairment like AD.

Of course, this isn’t an exhaustive list, but it’s a good place to start and points me in the right direction for what to work on next. Stay tuned!

*Editor’s Note:*[ *Join Heartbeat on Slack*](http://bit.ly/heartbeatslack) *and follow us on*[ *Twitter*](https://twitter.com/fritzlabs) *and*[ *LinkedIn*](https://www.linkedin.com/company/fritz-labs-inc/) *for the all the latest content, news, and more in machine learning, mobile development, and where the two intersect.*

<iframe frameborder="0" height="400" scrolling="no" src="https://cdn.embedly.com/widgets/media.html?src=https://heartbeat.fritz.ai/https%3A%2F%2Fupscri.be%2Fdfdb75%3Fas_embed%3Dtrue&dntp=1&url=https%3A%2F%2Fupscri.be%2Fdfdb75%2F&image=http%3A%2F%2Fapi.screenshotlayer.com%2Fapi%2Fcapture%3Faccess_key%3Dfe59908dad3baab69ffab249a2224b03%26viewport%3D1024x612%26width%3D1000%26url%3Dhttps%253A%252F%252Fupscri.be%252Fdfdb75%253Fscreenshot&key=d04bfffea46d4aeda930ec88cc64b87c&type=text%2Fhtml&schema=upscri%22 width="><https://medium.com/media/05616eaceabf5537ffbda5b6811c367c/href></iframe>![](https://medium.com/_/stat?event=post.clientViewed&referrerSource=full_rss&postId=f538d2d9507a)- - - - - -

[How Dementia Affects Conversation: Building a More Accessible Conversational AI](https://heartbeat.fritz.ai/how-dementia-effects-conversation-f538d2d9507a) was originally published in [Heartbeat](https://heartbeat.fritz.ai/) on Medium, where people are continuing the conversation by highlighting and responding to this story.