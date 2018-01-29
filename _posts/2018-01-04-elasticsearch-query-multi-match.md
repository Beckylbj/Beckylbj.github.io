---
layout: post
title:  "elasticsearch multi match query(多字段查询)"
crawlertitle: "elasticsearch"
summary: "How to query in elasticsearch"
date:   2018-01-04
categories: posts
tags: 'Elasticsearch-1.7.6'
author: Becky
---

<h5>允许多个字段的查询</h5>

```
    {
        "multi_match" : {
            "query":    "this is a test", 
            "fields": [ "subject", "message" ] 
        }
    }

    {
        "multi_match" : {
            "query":    "Will Smith",
            "fields": [ "title", "*_name" ] 
        }
    }
```