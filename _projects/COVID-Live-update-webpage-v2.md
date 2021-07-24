---
title: "COVID Live update webpage Version2"
image: 
  path: /assets/images/COVID-v2.jpg
  thumbnail: /assets/images/COVID-v2.jpg
  caption: "version2 webpage main page."
categories: 
  - COVID-Webpage
tags:
  - In progress
  - version2
  - Webpage
  - ETL
last_modified_at: 2021-07-24 12:00:00 +0100
---

# [Demo Page](https://johnjongyoonkim.eu.ngrok.io/)

## Source Codes

* [**FrontEnd**](https://github.com/ArtemisDicoTiar/winery/tree/feature/10/covid_tmp)
* [**BackEnd(API)**](https://github.com/ArtemisDicoTiar/covid_data_blog)
* [**Data Analysis**](https://github.com/ArtemisDicoTiar/MEDIC)
* [**Airflow ETL dags (private)**](https://github.com/ArtemisDicoTiar/dags)

## Explanation

After studying about technology stacks especially on web development. Various tech stacks are applied for better performance and visualisation.

Continuing from version1 statis webpage, this project provides dynamic region search, openAPI, and better forecasting performance.

## Technology Stacks

* Web
  * Hosting
    * Nginx (reverse proxy) + Nginx (in docker)
  * FrontEnd
    * Vuejs (with Vuex, JavaScript)
  * BackEnd
    * python: Flask, Django
* Server
  * Database: MariaDB (MySQL equivalent)
  * Data pipeline: Airflow ETL (python)
    * **Celery** worker applied for parallel processing (Rabbit-mq)
  * Deployment 
    * Environment: Docker, Docker-compose, Kubernetes(Experiment)
    * CI/CD: Jenkins

### Web

Now FrontEnd and BackEnd both are built and hosted. Both applications are hosted via nginx in docker and nginx on host device (Raspberry pi 4, RPi) for reverse-proxy.

FrontEnd is built with Vuejs for dynamic action and data represented on frontend view is requested via implemented BackEnd, REST API.

BackEnd is initially built with flask as its framework is light to use. However, due to the endpoint for this project is increase because the type of data is added, therefore organised new BackEnd API is built with django-rest framework.

### Server

MariaDB is used for this project's Database as most of data format fits into relational table.

The data pipeline to crawl, processing, forecast/prediction, post-processing various format of origin data is built with python and run on Airflow1.10 ETL. To run multiple DAGs in parallel, rabbit-mq is installed and used via celery worker.

The deployment process is triggered with CI/CD tool, Jenkins. The Jenkins is installed and connected to each github repository. To deploy application in clear environment, Docker image is built and its image run on the container. For better deployment process and performance, Kubernetes server (1 RPi4 main, 7 RPi 3 compute module subs) is being tested and experimented.

## Update List 

Update list before this blog is built is written on [this page](https://johnjongyoonkim.eu.ngrok.io/updates).

Further updates are going to be listed below and linked page.
