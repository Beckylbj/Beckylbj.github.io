---
layout: post
title:  "elasticsearch match query"
crawlertitle: "elasticsearch"
summary: "How to query in elasticsearch"
date:   2017-12-28
categories: posts
tags: 'Elasticsearch-1.7.6'
author: Becky
---
<h5>The default match query type is boolean type. </h5>

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

* operator, this flag can be set to or or and, default is or.

```
下面两个query是等价的

    {
        "query":{
            "match" : {
                "title": "brown fox"
            }
        }
    }

    {
        "query":{
            "bool": {
                "should": [
                    { "term": { "title": "brown" }},
                    { "term": { "title": "fox"   }}
                ]
            }
        }
    }
```

```
下面两个query是等价的

    {
        "query":{
            "match" : {
                "title": "brown fox",
                "operator":"and"
            }
        }
    }

    {
        "query":{
            "bool": {
                "must": [
                    { "term": { "title": "brown" }},
                    { "term": { "title": "fox"   }}
                ]
            }
        }
    }
```

* minimum_should_match 指定最少匹配多少

```
    {
        "query":{
            "match" : {
                "title": "quick brown fox",
                "minimum_should_match":"75%"
            }
        }
    }

    {
        "query":{
            "bool": {
                "should": [
                    { "term": { "title": "quick" }},
                    { "term": { "title": "brown" }},
                    { "term": { "title": "fox"   }}
                ],
                "minimum_should_match":2
            }
        }
    }
    因为只有3个查询语句，minimum_should_match的值75%会被向下舍入到2。即至少两个should语句需要匹配。
```

* zero_terms_query, can be set to none or all, default is none. The all is corresponds to a match all query.
