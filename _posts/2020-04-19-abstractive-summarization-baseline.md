---
title: 'Abstractive Summarization Baseline Model'
date: 2020-04-29
permalink: /posts/2020/04/abstractive-summarization-baseline/
tags:
  - IR
  - NLP
  - Chinese
---


> 这篇blog想整理一下有哪些baseline model会用于abstractive summarization任务之中。

模型从ACL 2019和abstractive summarization相关的论文中总结出，包括了几乎所有在论文中被用作baseline的模型。

## ABS

- Reference: Alexander M. Rush, Sumit Chopra, and Jason Weston. 2015. A neural attention model for abstractive sentence summarization. In Proceedings of the 2015 Conference on Empirical Methods in Natural Language Processing, pages 379–389.
- Link: https://arxiv.org/pdf/1509.00685.pdf
- Github: https://github.com/facebookarchive/NAMAS
- We need a Tensorflow/PyTorch-based version for this



## CoreRank

- Reference: Guokan Shang, Wensi Ding, Zekun Zhang, Antoine Jean-Pierre Tixier, Polykarpos Meladianos, Michalis Vazirgiannis, and Jean-Pierre Lorre. 2018. Unsupervised abstractive meeting summarization with multi-sentence compression and budgeted submodular maximization. In Proceedings of the 56th Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers), volume 1.
- Link: https://www.aclweb.org/anthology/P18-1062.pdf



## Featseq2seq

- Reference: Ramesh Nallapati, Bowen Zhou, Cicero dos Santos, Caglar Gulcehre, and Bing Xiang. 2016. Abstractive text summarization using sequence-to-sequence rnns and beyond. In Proceedings of The 20th SIGNLL Conference on Computational Natural Language Learning, pages 280–290.
- Link: https://arxiv.org/pdf/1602.06023.pdf
- PyTorch-based program is in progress on Github. (https://github.com/JRC1995/Abstractive-Summarization)



## FTSum

- Reference: Ziqiang Cao, Furu Wei, Wenjie Li, and Sujian Li. 2018b. Faithful to the original: Fact aware neural abstractive summarization. In Thirty-Second AAAI Conference on Artificial Intelligence.
- Link: https://arxiv.org/pdf/1711.04434.pdf



## GLEAM

- Reference: Yang Gao, Yang Wang, Luyang Liu, Yidi Guo, and Heyan Huang. 2019. Neural abstractive summarization fusing by global generative topics. Neural Computing and Applications.
- Link: https://link.springer.com/content/pdf/10.1007/s00521-018-3946-7.pdf
- Github link: https://github.com/AEGISEDGE/GLEAM



## KL-Sum

- Reference: Aria Haghighi and Lucy Vanderwende. 2009. Exploring content models for multi-document summarization. In Proceedings of the North American Chapter of the Association for Computational Linguistics (NAACL)
- Link: https://www.aclweb.org/anthology/N09-1041.pdf



## LexRank

- Reference: Gunes Erkan and Dragomir R. Radev. 2004. LexRank: Graph-based lexical centrality as salience in text summarization. Journal of Artificial Intelligence Research.
- Link: https://www.aaai.org/Papers/JAIR/Vol22/JAIR-2214.pdf
- Github link: https://github.com/crabcamp/lexrank



## Open-NMT

- Reference: Guillaume Klein, Yoon Kim, Yuntian Deng, Jean Senellart, and Alexander Rush. 2017. Opennmt: Open-source toolkit for neural machine translation. Proceedings of ACL 2017, System Demonstrations, pages 67–72.
- Link: https://arxiv.org/pdf/1701.02810.pdf
- Github link: https://github.com/OpenNMT/OpenNMT-py



## PGN

- Reference: Abigail See, Peter J Liu, and Christopher D Manning. 2017. Get to the point: Summarization with pointergenerator networks. In Proceedings of the 55th Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers), volume 1, pages 1073–1083.
- Link: https://arxiv.org/pdf/1704.04368.pdf
- Github: https://github.com/abisee/pointer-generator



## RAS-Elman

- Reference: Sumit Chopra, Michael Auli, and Alexander M. Rush. 2016. Abstractive sentence summarization with attentive recurrent neural networks. In Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies, pages 93–98.
- Link: https://www.aclweb.org/anthology/N16-1012.pdf



## R3Sum

- Reference: Ziqiang Cao, Wenjie Li, Sujian Li, and Furu Wei. 2018a. Retrieve, rerank and rewrite: Soft template based neural summarization. In Proceedings of the 56th Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers), volume 1, pages 152–161.
- Link: https://www.aclweb.org/anthology/P18-1015.pdf



## RNN Language Model

- Reference: Ilya Sutskever, James Martens, and Geoffrey E Hinton. 2011. Generating text with recurrent neural networks. In Proceedings of the 28th International Conference on Machine Learning (ICML-11), pages 1017–1024. JMLR.org
- Link: http://www.icml-2011.org/papers/524_icmlpaper.pdf
- Github: https://github.com/minimaxir/textgenrnn

### Feature

- The output is fluent in English
- The content is not related to our task



## SEASS

- Reference: Qingyu Zhou, Nan Yang, Furu Wei, and Ming Zhou. 2017. Selective encoding for abstractive sentence summarization. In Proceedings of the 55th Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers), pages 1095– 1104.
- Link: https://arxiv.org/pdf/1704.07073.pdf
- Github link: https://github.com/toru34/zhou_acl_2017



## S2S+CGU

- Reference: Junyang Lin, Sun Xu, Shuming Ma, and Qi Su. 2018. Global encoding for abstractive summarization. In Proceedings of the 56th Annual Meeting of the Association for Computational Linguistics (Volume 2: Short Papers), pages 163–169.
- Link: https://www.aclweb.org/anthology/P18-2027.pdf
- Github link: https://github.com/lancopku/Global-Encoding



## SumBasic

- Reference: Lucy Vanderwende, Hisami Suzuki, Chris Brockett, and Ani Nenkova. 2007. Beyond SumBasic: Taskfocused summarization with sentence simplification and lexical expansion. Information Processing and Management, 43(6):1606–1618.
- Link: https://www.cis.upenn.edu/~nenkova/papers/ipm.pdf



## Other baselines

### Seq2seq+LSTM+Local Attention

- Github link: https://github.com/JRC1995/Abstractive-Summarization

