---
layout: post
title:  "elasticsearch query"
crawlertitle: "elasticsearch"
summary: "How to query in elasticsearch"
date:   2017-12-28
categories: posts
tags: 'Elasticsearch-1.7.6'
author: Becky
---
##### Query all
```
    curl -XGET http://ip:9200/indexname/typename/_search
```
##### Query type mapping
```
    curl -XGET http://ip:9200/indexname/typename/_mapping
```
##### Query by id
```
    curl -XGET http://ip:9200/indexname/typename/{_id}
```

