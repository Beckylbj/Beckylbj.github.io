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
##### match Query

* boolean type. The default match query type, 
```
    curl -XPOST http://ip:9200/indexname/typename/_search 

    {
        "query":{
            "match" : {
                "message" : "this is a test"
            }
        }
    }
```
