---
title: 'Abstractive Summarization Baseline Model'
date: 2020-04-19
permalink: /posts/2020/04/abstractive-summarization-baseline/
tags:
  - IR
  - NLP
  - English
---


> This bloh tries to summary those baselines models used for abstractive summarization task.

Based on the [papers related to abstractive summarization in the proceedings of ACL 2019](https://chz816.github.io/posts/2020/04/acl-2019-papers/), this blog tries to conclude almost every baseline models used in those papers.

# Overview

| Model             | Cited by # | Year |
| ----------------- | ---------- | ---- |
| ABS               | 1376       | 2015 |
| CoreRank          | 14         | 2018 |
| Featseq2seq       | 738        | 2016 |
| FTSum             | 49         | 2018 |
| GLEAM             | ?          | 2019 |
| KL-Sum            | 453        | 2019 |
| LexRank           | 2286       | 2004 |
| Open-NMT          | 697        | 2017 |
| PGN               | 667        | 2017 |
| RAS-Elman         | 434        | 2016 |
| R3Sum             | 38         | 2018 |
| RNN Langage Model | 1073       | 2011 |
| SEASS             | 127        | 2017 |
| S2S+CGU           | 50         | 2018 |
| SumBasic          | 246        | 2007 |

## ABS

- Reference: Rush, A. M., Chopra, S., & Weston, J. (2015). A neural attention model for abstractive sentence summarization. *arXiv preprint arXiv:1509.00685*.
- Link: https://arxiv.org/pdf/1509.00685.pdf
- Github: https://github.com/facebookarchive/NAMAS
- We need a Tensorflow/PyTorch-based version for this

### About Paper

This paper proposes sentence-level abstractive summarization approach: generate each word of the summary conditioned on the input sentence.

### Method

#### Encoder

##### Bag-of-Words Encoder

Use the bag-of-words of the input sentence, to capture the relative importance of words to distinguish content words.

##### Convolutional Encoder

Improve the representations from bag-of-words encoder by allowing local interactions between words: explore the relationships between words.

##### Attention-based Encoder

- Replace the uniform distribution in bag-of-words with a learned soft alignment between input and summary.
- The soft alignment is then used to weight the smoothed version of the input to construct the representation.

#### Training

Minimize the negative log-likehood by mini-batch stochastic gradient descent.

#### Decoder

Beam search: maintain the full vocabulary while limiting itself to several potential hypothesis.



## CoreRank

- Reference: Shang, G., Ding, W., Zhang, Z., Tixier, A. J. P., Meladianos, P., Vazirgiannis, M., & Lorré, J. P. (2018). Unsupervised abstractive meeting summarization with multi-sentence compression and budgeted submodular maximization. *arXiv preprint arXiv:1805.05271*.
- Link: https://www.aclweb.org/anthology/P18-1062.pdf



## Featseq2seq

- Reference: Nallapati, R., Zhou, B., Gulcehre, C., & Xiang, B. (2016). Abstractive text summarization using sequence-to-sequence rnns and beyond. *arXiv preprint arXiv:1602.06023*.
- Link: https://arxiv.org/pdf/1602.06023.pdf
- PyTorch-based program is in progress on Github. (https://github.com/JRC1995/Abstractive-Summarization)



## FTSum

- Reference: Cao, Z., Wei, F., Li, W., & Li, S. (2018, April). Faithful to the original: Fact aware neural abstractive summarization. In *Thirty-Second AAAI Conference on Artificial Intelligence*.
- Link: https://arxiv.org/pdf/1711.04434.pdf



## GLEAM

- Reference: Gao, Y., Wang, Y., Liu, L., Guo, Y., & Huang, H. (2019). Neural abstractive summarization fusing by global generative topics. *Neural Computing and Applications*, 1-10.
- Link: https://link.springer.com/content/pdf/10.1007/s00521-018-3946-7.pdf
- Github link: https://github.com/AEGISEDGE/GLEAM



## KL-Sum

- Reference: Haghighi, A., & Vanderwende, L. (2009, June). Exploring content models for multi-document summarization. In *Proceedings of Human Language Technologies: The 2009 Annual Conference of the North American Chapter of the Association for Computational Linguistics* (pp. 362-370).
- Link: https://www.aclweb.org/anthology/N09-1041.pdf



## LexRank

- Reference: Erkan, G., & Radev, D. R. (2004). Lexrank: Graph-based lexical centrality as salience in text summarization. *Journal of artificial intelligence research*, *22*, 457-479.
- Link: https://www.aaai.org/Papers/JAIR/Vol22/JAIR-2214.pdf
- Github link: https://github.com/crabcamp/lexrank

### About Paper

This paper targets at the extractive summarization task for multi-document.

The fundemental approach is to measure the centrality of each sentence and extract the important ones as for summarization.

### Approach

#### Traditional Centroid-based Summarization

Definition："*A common way of assessing word centrality is to look at the centroid of the document cluster in a vector space*".

In centroid-based summarization proposed by [Radev, Jing & Buudziknowska (2000)](https://arxiv.org/pdf/cs/0005020.pdf), if this sentence contains more words from the centroid of this cluster, this sentence is considered as more **central**. This appraoch measures if the sentence is closed to the centroid of the cluster.

#### New Centrality-based Sentence Salience

Borrowed the idea of *prestige* in social network analysis, this paper claims that "a cluster of documents can be viewed as a network of sentences that are related to each other". So if two documents are sharing the same topic, they are expected to be closer to each other in the graph.

This paper uses the bag-of-words model to represent each sentence to a vector. Based on this, the similarity between two documents are calculated as the cosine distance. A cluster of documents could be represented by a cosine similarity matrix where each entry in the matrix is the similarity score.

#### Degree

To remove some insignificant similarity between documents from the matrix, this paper defines a threshold to map the cosine similarity matrix to an undirected graph: each node corresponds to one document, and the edge between nodes is significantly similarity between two documents.

A simple way to implement this approach is to count the number of similar sentences for each sentence.

- Too low thresholds may mistakenly take weak similarities into consideration
- Too high thresholds may lose many of the similarity relations in a cluster

#### LexRank with Threshold

This approach considers an important theory in social network analysis: even if we have a graph, each edge should not contribute exactly the same to the node. When we summarize the sentence/document, each word in the sentence/document is playing different roles.

To solve this problem, the paper proposes to consider "the centrality of the voting nodes into account in weighting each vote". A straightforward way is to assume every node having a centrality value based on its importance level. This value is distributed to its neighbor through the edge connection.

#### Continus LexRank

Using the binary discretization on the cosine matrix leads to an unweighted graph. One improvement over LexRank is to use the strength of the similarity links. When computing LexRank for a sentence, we need to multiply the LexRank values of the linking sentences by the weights of the links: these weights are normalized by the row sums.



## Open-NMT

- Reference: Klein, G., Kim, Y., Deng, Y., Senellart, J., & Rush, A. M. (2017). Opennmt: Open-source toolkit for neural machine translation. *arXiv preprint arXiv:1701.02810*.
- Link: https://arxiv.org/pdf/1701.02810.pdf
- Github link: https://github.com/OpenNMT/OpenNMT-py



## PGN

- Reference: See, A., Liu, P. J., & Manning, C. D. (2017). Get to the point: Summarization with pointer-generator networks. *arXiv preprint arXiv:1704.04368*.
- Link: https://arxiv.org/pdf/1704.04368.pdf
- Github: https://github.com/abisee/pointer-generator



## RAS-Elman

- Reference: Chopra, S., Auli, M., & Rush, A. M. (2016, June). Abstractive sentence summarization with attentive recurrent neural networks. In *Proceedings of the 2016 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies* (pp. 93-98).
- Link: https://www.aclweb.org/anthology/N16-1012.pdf



## R3Sum

- Reference: Cao, Z., Li, W., Li, S., & Wei, F. (2018, July). Retrieve, rerank and rewrite: Soft template based neural summarization. In *Proceedings of the 56th Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)* (pp. 152-161).
- Link: https://www.aclweb.org/anthology/P18-1015.pdf



## RNN Language Model

- Reference: Sutskever, I., Martens, J., & Hinton, G. E. (2011). Generating text with recurrent neural networks. In *Proceedings of the 28th international conference on machine learning (ICML-11)* (pp. 1017-1024).
- Link: http://www.icml-2011.org/papers/524_icmlpaper.pdf
- Github: https://github.com/minimaxir/textgenrnn

### About Paper

- Note: this paper is not designed for summarization task. It is more like a random generation.

### Feature

- The output is fluent in English
- The content is not related to our task



## SEASS

- Reference: Zhou, Q., Yang, N., Wei, F., & Zhou, M. (2017). Selective encoding for abstractive sentence summarization. *arXiv preprint arXiv:1704.07073*.
- Link: https://arxiv.org/pdf/1704.07073.pdf
- Github link: https://github.com/toru34/zhou_acl_2017



## S2S+CGU

- Reference: Lin, J., Sun, X., Ma, S., & Su, Q. (2018). Global encoding for abstractive summarization. *arXiv preprint arXiv:1805.03989*.
- Link: https://www.aclweb.org/anthology/P18-2027.pdf
- Github link: https://github.com/lancopku/Global-Encoding



## SumBasic

- Reference: Vanderwende, L., Suzuki, H., Brockett, C., & Nenkova, A. (2007). Beyond SumBasic: Task-focused summarization with sentence simplification and lexical expansion. *Information Processing & Management*, *43*(6), 1606-1618.
- Link: https://www.cis.upenn.edu/~nenkova/papers/ipm.pdf



## Other baselines

### Seq2seq+LSTM+Local Attention

- Github link: https://github.com/JRC1995/Abstractive-Summarization

