---
layout:     post
title:      Abstractive Summarization常用的数据集
subtitle:   关于数据集的基本信息介绍
date:       2020-04-13
author:     Rachel
header-img: img/post-bg-os-metro.jpg
catalog: true
tags:
    - IR
    - NLP
    - Chinese
    - dataset
---

> 这篇blog尝试总结了一下abstractive summarization常用的数据集。

# 新闻类常用的数据集

| Dataset  |  # doc  |
| :------: | :-----: |
|  CNN/DM  | 311971  |
| Gigaword | 3995559 |
|   XSUM   | 226183  |
| DUC 2003 |  ~1260  |
| DUC 2004 |  ~1250  |



## CNN/DM

> 链接：https://github.com/abisee/cnn-dailymail

包括约30万新闻文章，数据集一共有两个特征：新闻文章和highlights。

- 已经被包括在tensorflow.datasets中

数据举例：

```
{'article': <tf.Tensor: shape=(), dtype=string, numpy=b"By . Associated Press . PUBLISHED: . 14:11 EST, 25 October 2013 . | . UPDATED: . 15:36 EST, 25 October 2013 . The bishop of the Fargo Catholic Diocese in North Dakota has exposed potentially hundreds of church members in Fargo, Grand Forks and Jamestown to the hepatitis A virus in late September and early October. The state Health Department has issued an advisory of exposure for anyone who attended five churches and took communion. Bishop John Folda (pictured) of the Fargo Catholic Diocese in North Dakota has exposed potentially hundreds of church members in Fargo, Grand Forks and Jamestown to the hepatitis A . State Immunization Program Manager Molly Howell says the risk is low, but officials feel it's important to alert people to the possible exposure. The diocese announced on Monday that Bishop John Folda is taking time off after being diagnosed with hepatitis A. The diocese says he contracted the infection through contaminated food while attending a conference for newly ordained bishops in Italy last month. Symptoms of hepatitis A include fever, tiredness, loss of appetite, nausea and abdominal discomfort. Fargo Catholic Diocese in North Dakota (pictured) is where the bishop is located .">, 'highlights': <tf.Tensor: shape=(), dtype=string, numpy=b'Bishop John Folda, of North Dakota, is taking time off after being diagnosed .\nHe contracted the infection through contaminated food in Italy .\nChurch members in Fargo, Grand Forks and Jamestown could have been exposed .'>}
```



## Gigaword

> 链接：https://www.tensorflow.org/datasets/catalog/gigaword

包括约400万的新闻文章，其中数据集使用headline作为这篇新闻报道的summary。数据集中共包括两个变量：文章和摘要。

- 已经被包括在tensorflow.datasets中

```
FeaturesDict({
    'document': Text(shape=(), dtype=tf.string),
    'summary': Text(shape=(), dtype=tf.string),
})
```

数据举例：

```
{'document': <tf.Tensor: shape=(), dtype=string, numpy=b'a lung infection that killed two people and sickened ## in just a few days was transmitted by a pet parrot , a health official said thursday .'>, 'summary': <tf.Tensor: shape=(), dtype=string, numpy=b'tests show that illness killing two sickening ## in croatia was'>}

{'document': <tf.Tensor: shape=(), dtype=string, numpy=b"british candy maker cadbury plc on tuesday accepted and recommended to shareholders kraft 's improved takeover offer worth $ ##.# billion , potentially ending a months-long corporate battle to create the world 's largest maker of chocolate and sweets .">, 'summary': <tf.Tensor: shape=(), dtype=string, numpy=b'kraft foods cadbury agree $ ##.# bln deal'>}
```



## DUC 2003/2004

> 链接：https://duc.nist.gov/duc2003/tasks.html， https://duc.nist.gov/duc2004/

DUC系列的数据集使用的是新闻类的文档（来自TREC和TDT）。

- DUC 2003中包括了
  - 30个TREC Document Clusters
  - 30个TDT Document Clusters
  - 30个Novelty Track Document Clusters
- DUC 2004中包括了
  - 50个TDT English Document Clusters
  - 25个TDT Arabic Document Clusters
  - 50 TREC English Document Clusters

Document:

```
Cambodia's ruling party responded Tuesday to criticisms of its leader in the U.S. Congress with a lengthy defense of strongman Hun Sen's human rights record. The Cambodian People's Party criticized a non-binding resolution passed earlier this month by the U.S. House of Representatives calling for an investigation into violations of international humanitarian law allegedly committed by Hun Sen. Events mentioned in the resolution include Hun Sen's coup last year against his co-prime minister, Prince Norodom Ranariddh, and his violent crackdown in September against anti-government demonstrations. A copy of the resolution has since been submitted to the U.S. Senate Committee on Foreign Relations. ...
```

Summary：

```
Cambodian prime minister Hun Sen rejects demands of 2 opposition parties for talks in Beijing after failing to win a 2/3 majority in recent elections.
Sihanouk refuses to host talks in Beijing.
Opposition parties ask the Asian Development Bank to stop loans to Hun Sen's government.
CCP defends Hun Sen to the US Senate.
FUNCINPEC refuses to share the presidency.
Hun Sen and Ranariddh eventually form a coalition at summit convened by Sihanouk.
Hun Sen remains prime minister, Ranariddh is president of the national assembly, and a new senate will be formed.
Opposition leader Rainsy left out.
He seeks strong assurance of safety should he return to Cambodia.
```



## XSUM

> 链接：https://www.tensorflow.org/datasets/catalog/xsum

使用来自BBC的新闻文章，数据集包括两个特征：文章和对应的一句话的摘要。

- 已经被包括在tensorflow.datasets中（但是需要手动下载）

```
FeaturesDict({
    'document': Text(shape=(), dtype=tf.string),
    'summary': Text(shape=(), dtype=tf.string),
})
```



# 跨domain可用的数据集

|      Dataset       |    # doc    |
| :----------------: | :---------: |
|        How2        |   ~80000    |
| AMI Meeting Corpus | ～200（？） |

## How2

> 链接：https://github.com/srvk/how2-dataset

How2数据集中包括了大概80000个视频，以及其对应的英文字母和摘要，共大概2000小时。



## AMI Meeting Corpus

> 链接：http://groups.inf.ed.ac.uk/ami/corpus/

数据集包括了大约100小时的会议视屏记录，每次大约30分钟，共4位参与者。