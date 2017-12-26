---
layout: post
title:  "elasticsearch install"
crawlertitle: "Hello"
summary: "default page"
date:   2017-12-26 11:10:00
categories: posts
tags: 'Elasticsearch - 1.7.6'
author: Becky
---
##### Elasticsearch 是一个实时的分布式搜索分析引擎

* 安装jdk
* download from [Elasticsearch download](https://www.elastic.co/downloads/elasticsearch "Elasticsearch download") 
    * curl -L -o http://download.elasticsearch.org/PATH/TO/VERSION.zip
    * unzip elasticsearch-$VERSION.zip
    * cd elasticsearch-$VERSION
* 启动elasticsearch
    * ./bin/elasticsearch
* 访问ES
    * curl 'http://localhost:9200/?pretty'
* 访问返回 
 ```
    {
        "status": 200,
        "name": "Jimmy Woo",
        "cluster_name": "elasticsearch",
        "version": {
            "number": "1.7.6",
            "build_hash": "c730b59357f8ebc555286794dcd90b3411f517c9",
            "build_timestamp": "2016-11-18T15:21:16Z",
            "build_snapshot": false,
            "lucene_version": "4.10.4"
        },
        "tagline": "You Know, for Search"
    }
```