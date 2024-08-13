---
title: "DADA: Distribution-Aware Domain Adaptation of PLMs for Information Retrieval"
image: 
  path: /assets/images/dada-thumbnail.png
  thumbnail: /assets/images/dada-thumbnail.png
  caption: "Findings of ACL 2024"
categories: 
  - Publication
tags:
  - ACL
  - Findings
last_modified_at: 2024-07-31 12:00:00 +0900
date: 2024-07-31 12:00:00 +0900
---

# Summary
This research tackles domain adaptation in information retrieval, where previous methods neglects the domain level information, such as IDF.


# Abstraction
Pre-trained language models (PLMs) exhibit promise in retrieval tasks but struggle with out-of-domain data due to distribution shifts. Addressing this, generative domain adaptation (DA), known as GPL, tackles distribution shifts by generating pseudo queries and labels to train models for predicting query-document relationships in new domains. However, it overlooks the domain distribution, causing the model to struggle with aligning the distribution in the target domain. We, therefore, propose a \textbf{\oursfull} (\ours) to guide the model to consider the domain distribution knowledge at the level of both a single document and the corpus, which is referred to as observation-level feedback and domain-level feedback, respectively. Our method effectively adapts the model to the target domain and expands document representation to unseen gold query terms using domain and observation feedback, as demonstrated by empirical results on the BEIR benchmark.

# Details
* This paper is sponsored by SNU-NAVER Hyperscale AI Center, MIST (IITP, South Korea Government).

## Paper
* ACL-Anthology: [🔗 Official Link](https://aclanthology.org/2024.findings-acl.825/)

## Code
[**Source Code**](https://github.com/ldilab/DADA)
