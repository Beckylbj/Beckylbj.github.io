---
layout: post
title:  "elasticsearch filtered query(过滤器查询)"
crawlertitle: "elasticsearch"
summary: "How to query in elasticsearch"
date:   2018-01-29
categories: posts
tags: 'Elasticsearch-1.7.6'
author: Becky
---
<h5>可以含有查询也可以含有别的filter</h5>

```
    {
        "query":{
            "filtered": {
                "query": {
                    "match": { "tweet": "full text search" }
                },
                "filter": {
                    "range": { "created": { "gte": "now-1d/d" }}
                }
            }
        }
    }
```

* multiple filters(多个过滤器可以被包装在一个bool里)
```
    {
        "query":{
            "filtered": {
                "query": { "match": { "tweet": "full text search" }},
                "filter": {
                    "bool": {
                        "must": { "range": { "created": { "gte": "now-1d/d" }}},
                        "should": [
                            { "term": { "featured": true }},
                            { "term": { "starred":  true }}
                        ],
                        "must_not": { "term": { "deleted": false }}
                    }
                }
            }
        }
    }
```

* Filter strategyedit

You can control how the filter and query are executed with the strategy parameter:
```
{
    "filtered" : {
        "query" :   { ... },
        "filter" :  { ... },
        "strategy": "leap_frog"
    }
}
```

<h5><font color=RED>This is an expert-level setting. Most users can simply ignore it.</font></h5>

The strategy parameter accepts the following options:

<table>
    <tr>
        <th>leap_frog_query_first</th>
        <th>Look for the first document matching the query, and then alternatively advance the query and the filter to find common matches.</th>
    </tr>
    <tr>
        <th>leap_frog_filter_first</th>
        <th>Look for the first document matching the filter, and then alternatively advance the query and the filter to find common matches.</th>
    </tr>
    <tr>
        <th>leap_frog</th>
        <th>Same as leap_frog_query_first.</th>
    </tr>
    <tr>
        <th>query_first</th>
        <th>If the filter supports random access, then search for documents using the query, and then consult the filter to check whether there is a match. Otherwise fall back to leap_frog_query_first.</th>
    </tr>
    <tr>
        <th>random_access_${threshold}</th>
        <th>If the filter supports random access and if there is at least one matching document among the first threshold ones, then apply the filter first. Otherwise fall back to leap_frog_query_first. ${threshold} must be greater than or equal to 1.</th>
    </tr>
    <tr>
        <th>random_access_always</th>
        <th>Apply the filter first if it supports random access. Otherwise fall back to leap_frog_query_first.</th>
    </tr>
</table>

The default strategy is to use query_first on filters that are not advanceable such as geo filters and script filters, and random_access_100 on other filters.