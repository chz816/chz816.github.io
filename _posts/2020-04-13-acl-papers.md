---
title: 'ACL 2019 Abstractive Summarization Papers'
date: 2020-04-13
permalink: /posts/2020/04/acl-2019-papers/
tags:
  - IR
  - NLP
  - Chinese
---

> ACL (Association for Computational Linguistics) 2019共有661篇文章入选proceedings。这篇blog记录一下本届ACL中和Abstractive Summarization相关的论文。



# 论文

## BiSET: Bi-directional Selective Encoding with Template for Abstractive Summarization

- 论文链接： https://www.aclweb.org/anthology/P19-1207.pdf
- GitHub链接：https://github.com/InitialBug/BiSET
- 整个framework包括3步：
  - Retrieve：返回备选的templates
    - 单纯注重文字level的匹配
    - 不考虑文字或者文章之间的联系
    - 直接使用了apache lucene (https://lucene.apache.org/)
  - Fast Rerank：选择最适合的template
    - 从深层语义角度来考量，决定最好的template
    - 1-D Convolution来捕捉n-gram的特征，使用glu作为激活函数，生成high-level representation。
  - BiSET：从文章和template中选择共有信息来生成摘要。
    - Template-to-Article (T2A): 利用template来筛选文章的representation
    - Article-to-Template (A2T): 选择部分的final article representation
    - Decoder layer: RNN

> Our model involves a novel bi-directional selective layer with two gates to mutually select key information from an article and its template to assist with summary generation.

- 数据：Gigaword dataset
  - https://github.com/harvardnlp/sent-summary
- 衡量：
  - ROUGE：衡量选中的template和summary的质量
  - NDCG：衡量Fast Rerank
  - performance比较：
    - 随机选择
    - Retrieve-top：在Retrieve步骤最好的
    - N-Optimal：top N



## Scoring Sentence Singletons and Pairs for Abstractive Summarization

- 论文链接：https://www.aclweb.org/anthology/P19-1209.pdf
- GitHub链接：https://github.com/ucfnlp/summarization-sing-pair-mix
-  从文章中选择句子，再对选中的句子进行改进。
  - 将文章中每个单个的句子，和每前后两句话筛选出来，称为instance
  - 对每个instance进行打分
    - 如果一个单个的句子包括了足够多的重要信息，单个句子应该得分比一对句子要高
  - 建立vector representation
    - 使用了BERT
      - 用classification task进行了fine tuning：判断instance中是否包含了人写的摘要中的句子
  - 将instances进行fusion和compression
- 数据：
  - XSUM：将新闻文章概括为一句话
    - 链接：https://github.com/EdinburghNLP/XSum/tree/master/XSum-Dataset
  - CNN/DM：将新闻文章概括为一段话（平均：4句）
    - 链接：https://github.com/abisee/cnn-dailymail
  - DUC-04：将10篇讨论同一个主题的文章进行该落（平均：5句）
    - 链接：https://www-nlpir.nist.gov/projects/duc/data.html
- 衡量：ROUGE



## Keep Meeting Summaries on Topic: Abstractive Multi-Modal Meeting Summarization

- 论文链接：https://www.aclweb.org/anthology/P19-1210.pdf
- 专注于对于会议进行摘要概括
- 首先对会议按照话题进行分割，再对每一个部分进行摘要概括
  - 数据包括：视频，ASR生成的文本
  - Visual Focus of Attention (VFOA)：根据每个会议参加者看向的方向来确定谁在说话
  - 将会议划分为不同的片段，每个片段有自己的主题
    - Encoder：会议transcript
    - Decoder：topic segmentation
      - 使用SegBot
  - 概括会议内容使用了Pointer-Generator Network (PGN)
- 数据：AMI Meeting Corpus
  - 每个视频是30分钟的会议，包括4位参会者
  - 链接：http://groups.inf.ed.ac.uk/ami/corpus/



## Zero-Shot Cross-Lingual Abstractive Sentence Summarization through Teaching Generation and Attention

- 论文链接：https://www.aclweb.org/anthology/P19-1305.pdf
- GitHub链接：https://github.com/KelleyYin/Cross-lingual-Summarization
- 侧重于概括+翻译：为文章提供另外一种语言的摘要概括
  - Teacher：同语言
  - Student：跨语言
  - Teacher和Student都使用了Transformer架构
- 数据：
  - Gigaword
  - DUC 2004



## Abstractive text summarization based on deep learning and semantic content generalization

- 论文链接：https://www.aclweb.org/anthology/P19-1501.pdf
- GitHub链接：https://github.com/pkouris/abtextsum
- 结合了深层学习的encoder-decoder结构和semantic-based data transformations
  - 首先进行text generalization对文本进行处理
    - Named Entities-driven Generalization (NEG)
    - Level-driven Generalization (LG)
  - 利用Seq2seq来生成摘要
  - 再处理：将笼统的通用词转化成为具体文本中具象词
- 数据：
  - Gigaword
  - DUC 2004



## Multimodal Abstractive Summarization for How2 Videos

- 论文链接：https://www.aclweb.org/anthology/P19-1659.pdf
- 目标：为视频和语音transcript提供流畅的文字摘要。
  - 为视频提供一段简短的摘要来概括视频中的重要信息

> Address this by aiming to generate a short text summary of the video that describes the most salient content of the video

- 使用了多资源的Seq2seq模型来整合信息，形成完整的输出。
  - Video-based：使用ResNeXt来提取视频中的特征
    - 输出是一个特征的序列（考虑到每16个不重叠的frames）
  - Speech-based：使用ASpIRE和EESEN
- 数据：How2，包括了2000小时的短视频，每个视频包括了human-generated transcript和2-3句的摘要概括
  - 链接：https://github.com/srvk/how2-dataset

