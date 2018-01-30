---
layout: post
title:  "elasticsearch fuzzy query(模糊查询)"
crawlertitle: "elasticsearch"
summary: "How to query in elasticsearch"
date:   2018-01-30
categories: posts
tags: 'Elasticsearch-1.7.6'
author: Becky
---
```
    {
        "query:{
            "fuzzy" : { "user" : "ki*" }
        }
    }
```
