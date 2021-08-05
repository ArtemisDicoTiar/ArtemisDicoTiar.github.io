---
title: "wisdomify -- storyteller"
image: 
  path: /assets/images/wisdomify_version0.jpg
  thumbnail: /assets/images/wisdomify_version0.jpg
  caption: "wisdomify demo version0"
categories: 
  - wisdomify
  - storyteller
  - SGM
tags:
  - In progress
last_modified_at: 2021-07-24 12:00:00 +0100
date: 2021-07-24 12:00:00 +0100
---

[**wisdomify**](https://github.com/eubinecto/wisdomify)
[**storyteller**](https://github.com/ArtemisDicoTiar/storyteller)

## Explanation

This project is building reverse-dictionary of korean proverb with BERT based model (wisdomify) and to train the model the datasets are prepared and crawled (storyteller).

## Technology Stacks

* wisdomify
  * pyTorch (python)
    * BERT based transformer model
  * Flask
    * Demo implementation
* storyteller
  * Selenium (python), request
    * crawling data

### wisdomify posts

Following bullet points are wisdomify related study, develop logs.

* [Version control for Dataset and model data (serialised file- eg → .ckpt, .pt, .mar)](https://github.com/eubinecto/wisdomify/issues/33)
  * Now wisdomify projects can control the version of dataset and model data.
* [Torch_serve for better model serving](https://github.com/eubinecto/wisdomify/issues/31)
  * Now wisdomify projects can serve various model with torch serve. However, the docker container cannot be deployed on ainize server as it only exposes one port where the torchserve requires at least 2.

### storyteller posts

Following bullet points are storyteller related study, develop logs.

* [DB controller via SSH tunnel](https://artemisdicotiar.github.io/cloud%20server/storyteller/2021/07/27/orcaleDB-python-controller.html)
  * Now storyteller can save crawled information to Orcale MySQL DB.
