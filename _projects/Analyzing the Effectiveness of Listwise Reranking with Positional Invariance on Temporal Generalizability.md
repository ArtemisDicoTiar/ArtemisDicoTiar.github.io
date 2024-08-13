---
title: "Analyzing the Effectiveness of Listwise Reranking with Positional Invariance on Temporal Generalizability"
image: 
  path: /assets/images/longeval2024-thumbnail.png
  thumbnail: /assets/images/longeval2024-thumbnail.png
  caption: "CLEF-WN 2024"
categories: 
  - Publication
tags:
  - CLEF
  - LongEval
last_modified_at: 2024-07-31 12:00:00 +0900
date: 2024-07-31 12:00:00 +0900
---

# Summary
This paper handles positional invariance in listwise reranking with temporal retrieval dataset.

The paper is accepted on CLEF-WN 2024, LongEval Lab.

This research is also being selected for conference travel sponsor awarded on 창의 자율 연구 1 (Creative and Independent AI Research 1) at Seoul National University.

# Abstraction
Benchmarking the performance of information retrieval (IR) methods are mostly conducted within a fixed set
of documents (static corpora). However, in real-world web search engine environments, the document set is
continuously updated and expanded. Addressing these discrepancies and measuring the temporal persistence
of IR systems is crucial. By investigating the LongEval benchmark, specifically designed for such dynamic
environments, our findings demonstrate the effectiveness of a listwise reranking approach, which proficiently
handles inaccuracies induced by temporal distribution shifts. Among listwise rerankers, our findings show that
ListT5, which effectively mitigates the positional bias problem by adopting the Fusion-in-Decoder architecture, is
especially effective, and more so, as temporal drift increases, on the test-long subset.

# Details
* This paper is being also submitted for assignment of 창의 자율 연구 1 (Creative and Independent AI Research 1) at Seoul National University.
* We are selected as top-30 students from whole research teams in the lecture supporting students travelling to any conference in 2024.
  * wishing to attend either EMNLP or AAAI.

## Paper
* Arxiv: [🔗 Link](https://arxiv.org/abs/2407.06716)
* CLEF-WN 2024 / LongEval: [🔗 Official Link](https://ceur-ws.org/Vol-3740/paper-221.pdf)

## Code
[**Source Code**](https://github.com/ldilab/longeval2024)
