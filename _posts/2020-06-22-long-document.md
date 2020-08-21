---
title: 'How to Handle Long Document'
date: 2020-06-22
permalink: /posts/2020/06/long-document/
tags:
  - NLP
  - Chinese
---



在使用RNN/LSTM来处理文本时，面对长文本，往往出现的问题是gradient vanish。

使用transformer来处理长文本时，往往有两种处理方式：

**方法1: 按“块”来处理长文本**

- [Multi-passage BERT](https://arxiv.org/pdf/1908.08167.pdf)

  在完成QA时：如果与这个问题相关的文章有$n$篇，那么模型往往会独立做$n$次预测。这样直接对比计算的分数是没有意义的。

  提出的模型一共分为两步：1. 选择相关的passages，2. 在所有选择中的相关文章中，整体来apply softmax

**方法2: 调整attention的计算**

之所以transformer无法计算太长的序列，根本原因就在于attention的计算。原始的attention计算公式是：
$$
Attention(Q,K,V)=softmax(\frac{QK^T}{\sqrt{d_K}})V
$$
针对一个长度为L的序列，attention的计算需要$O(L^2)$，这样的计算在较长的文本是需要极大的内存和算力要求。

![image-20200622144054432](/Users/rachelzheng/Documents/GitHub/chz816.github.io/_posts/img//image-20200622144054432.png)

​																	图片1: 来自[Longformer](https://arxiv.org/pdf/2004.05150v1.pdf)的figure 1

- [Transformer-XL](https://arxiv.org/pdf/1901.02860.pdf)

  “Instead of computing the hidden states from scratch for each new segment, we reuse the hidden states obtained in previous segments”

  针对普通版Transformer语言模型在训练阶段，各个segment缺乏联系的缺点，Transformer-XL给出的解决方法是在segment之间引入RNN机制，具体而言，就是把上一个segment计算好的hidden state进行存储，然后在计算下一个segment的时候，将上一个segment的这些信息作为一个context融入到当前segment的计算当中。

  上一个segment的hidden state沿着句子长度的方向与当前segment的hidden state进行concat，因此比如每个segment长度为4，那么concat之后长度就为8，然后再在这个concat过后的长度上进行Transformer Decoder操作，因此如果没有这种操作的话，那么每一个segment的开始第一个词实际上它的context信息只有第一个时刻的输入，而此时则能带上上一个segment的后三个词，体现在下图中的绿色线条。

  使用相对位置，舍弃了原模型中的绝对位置。

  ![image-20200622194733146](/Users/rachelzheng/Documents/GitHub/chz816.github.io/_posts/img//image-20200622194733146.png)

  ![image-20200622194751821](/Users/rachelzheng/Documents/GitHub/chz816.github.io/_posts/img//image-20200622194751821.png)

  ​			图2. Transformer和Transformer-XL的对比，来自Transformer-XL原文中的figure 1和figure 2

- [Reformer](https://arxiv.org/pdf/2001.04451.pdf)

Reformer提出利用locality-sensitive hashing(lsh)来将$O(L^2)$降低为$O(LlogL)$。Reformer主要做出了两点调整：

1. 调整attention的计算

   "Since softmax is dominated by the largest elements, for each query qi we only need to focus on the keys in K that are closest to qi."

   在公式1中我们可以看到，最消耗内存的计算是Q和K的点乘，而这个点乘的结果最后会被softmax函数处理。而根据softmax函数的特性，softmax的计算是被最大的元素所影响的。因此我们只需要找到了$K$中最靠近$q_i$的元素，就可以计算得出结果。

   而LSH正是被提出来在高维空间中寻找最相近的neighbors。 hashing scheme that assigns each vector x to a hash h(x) is called locality-sensitive if nearby vectors get the same hash with high probability and distant ones do not.

   Part (a) depicts that the attention matrix for full attention is typically sparse, but the computation does not take advantage of this sparsity. 

   In (b), the queries and keys have been sorted according to their hash bucket. Since similar items fall in the same bucket with high probability, the full attention pattern can be approximated by only allowing attention within each bucket.

   Hash buckets in this formulation tend to be uneven in size, which makes it difficult to batch across

   buckets. Moreover, the number of queries and the number of keys within a bucket may be unequal –

   in fact, it is possible for a bucket to contain many queries but no keys. We sort the queries by bucket number and, within each bucket, by sequence position; this defines a permutation where i 􏰂→ si after sorting. In the sorted attention matrix, pairs from the same bucket will cluster near the diagonal (as depicted in Figure 2c). 

   We can follow a batching approach where chunks of m consecutive queries (after sorting) attend to each other, and one chunk back (Figure 2d). 

   

   ![image-20200622151544852](/Users/rachelzheng/Documents/GitHub/chz816.github.io/_posts/img//image-20200622151544852.png)

   ​											图3. LSH Attention，此图为reformer论文中的figure 2

2. 使用reversible layer来调整

   “The main idea is to allow the activations at any given layer to be recovered from the activations at the following layer, using only the model parameters.”

- [Longformer](https://arxiv.org/pdf/2004.05150v1.pdf)

  - 使用sliding window：每次只考虑单词前后各$w/2$的token
  - 使用dilated sliding window：每个选中的token之间有间隔
  - 使用global attention：针对每个不同的下游任务

  ![image-20200622175314753](/Users/rachelzheng/Documents/GitHub/chz816.github.io/_posts/img//image-20200622175314753.png)

  ​											图4: Longformer，此图为longformer论文中的figure 2

**方法3: 两段式来处理文本**

