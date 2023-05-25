# Goggle

## Description

Goggle is the course project for CIS 555 Internet & Web Systems (Spring 2023) at the University of Pennsylvania. The project aimed to develop a Java-based distributed web search engine without any framework and deploy it on the cloud.

Contributors: Jinhui, Zihan, Kebin, Ruichen

The codes are made private due to course policy. For more information, please contact the author at ruichen199801@gmail.com.

## System Design

<img src="images/goggle-architecture.svg" alt="architecture" width="750">

The search engine comprises a web crawler, an indexer, and a frontend for ranking and query processing. These components are built on a custom HTTP/1.1 web server, a distributed key-value store (**KVS**), and a Spark-like distributed analytics engine (**Flame**).

The crawler initially crawled a corpus of 200K+ web pages. Next, the indexer executed parallel Flame jobs to compute the inverted index and PageRank scores. The computation results, along with filtered page information (URL, title, content), were stored as multiple table files in the KVS.

Lastly, the frontend handles queries by looking up search terms in the indexer, ranking results using TF-IDF/PageRank scores and other criteria, and returning the results on a user-friendly webpage resembling Google's style.

The crawling and indexing jobs were run both locally and on EC2 instances in several days. For the demo, the frontend, KVS master, and KVS workers were deployed on EC2 instances.

## Features

Some extra credit features were implemented to improve user-friendliness, such as infinite scrolling, spellcheck, cached pages, and image search. 

For instance, an LRU cache was implemented to optimize query performance for frequently searched terms. Additionally, the Azure Cognitive Service APIs were used to generate text summaries for photos uploaded by users.
