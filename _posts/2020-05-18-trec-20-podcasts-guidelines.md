---
title: 'TREC 2020 Podcasts Track Guidelines'
date: 2020-05-18
permalink: /posts/2020/05/trec-podcasts-guidelines/
tags:
  - IR
  - Chinese
---


> 这篇blog根据最新的TREC 2020 Podcasts Track Guidelines做一下中文的总结。

上周五最新放出了今年Podcasts Track的详细比赛指导，里面讨论了更多关于今年Podcasts Track的任务、衡量标准等信息。总体来说，和之前披露的相同的是，今年总共有两个任务：segment retrieval和summarization。

- 网页link：https://podcastsdataset.byspotify.com/

Guidelines首先强调了这个track存在的背景，也是目前以Spotify为首的流媒体公司所遇到的一些瓶颈问题。当下podcasts成为越来越流行的媒介形式，作为一种音频为主的媒介，怎样高效的从podcasts中检索到相关信息、或者重要信息成为一个难题。尽管一般来说podcast自身都会配有一段相关的介绍，但是这些介绍往往不能“完美”地概括出podcast中的内容。比如，有些介绍会指向其他的网站，如去youtube上关注我、或者在twitter上follow我等。同样，因为音频是主要的介质，在进行信息检索时往往是依靠字幕（ transcript）。因为各种的限制，也无法做到对于每个podcast都有完整的字幕。



## 任务1: 片段检索

任务1对应着片段检索（Fixed-length Segment Retrieval）。具体的要求是：给出一个query，期望可以返回和query最相关的2分钟长度的音频。

具体的topic会包含如下信息：

- topic的序列号（ topic number）
- topic的关键词query
- topic对应的详细解释（description）

例子如下：

``````html
<topic>

<num>1</num>

<query>Higgs boson</query>

<description>I’m looking for news and discussion about the discovery of the Higgs boson. When was it discovered? How? Who was involved? What are the implications of the discovery for physics?</description>

</topic> 
``````



### 衡量

任务1会由人工审核的方式来衡量模型的表现。NIST的评估人员会根据返回的2分钟片段给出四个等级的评价：

- Excellent：片段完美地切合了主题，对于观众来说是一个理想的起始点来收听。
- Good
- Fair
- Bad：返回片段和主题无关。



## 任务2: 概括

任务2侧重于对podcast中的内容进行概括。返回的摘要必须语意通顺，没有语法错误。理想中的应用背景是，用户可以根据这段概括，来判断是否要听这段podcast。所以这段摘要应该可以准确的概括出podcast中的信息，并且不会太长（这样可以保证在手机屏幕上可以阅读）。



### 评估集 (Evaluation Set)

评估集一共包含了500集的podcast，评审首先会人工审核podcast的发布者自己写的description，给出EGFB的等级划分。只有分到Excellent这个部分的podcast，才会拿出来使用。



### 测试集 (Test Set)

测试集包含共500集podcast，会在2020年六月给出。



### 衡量

今年会主要使用ROUGE来作为评判标准，具体对应的是unigram and bigram ROUGE-F。同样，考虑到summary应该足够简短，以至于可以在手机屏幕上阅读，也会只选择摘要的前200个词来进行新的一轮评估。