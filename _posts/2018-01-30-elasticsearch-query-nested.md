---
layout: post
title:  "elasticsearch nested query(嵌套查询)"
crawlertitle: "elasticsearch"
summary: "How to query in elasticsearch"
date:   2018-01-30
categories: posts
tags: 'Elasticsearch-1.7.6'
author: Becky
---
* 字段类型要是nested的
```
{
    "query":{
        "nested" : {
            "path" : "obj1",
            "score_mode" : "avg",
            "query" : {
                "bool" : {
                    "must" : [
                        {
                            "match" : {"obj1.name" : "blue"}
                        },
                        {
                            "range" : {"obj1.count" : {"gt" : 5}}
                        }
                    ]
                }
            }
        }
    }
}
```