---
layout: post
title:  "elasticsearch bool query(布尔类型query)"
crawlertitle: "elasticsearch"
summary: "How to query in elasticsearch"
date:   2018-01-04
categories: posts
tags: 'Elasticsearch-1.7.6'
author: Becky
---
<h5>组合布尔类型的查询</h5>

```
    {
        "bool" : {
            "must" :     [],
            "should" :   [],
            "must_not" : [],
        }
    }
```

* must 
```
    All of these clauses must match. The equivalent of AND.
```

* must_not 
```
    All of these clauses must not match. The equivalent of NOT.
```

* should 
```
    At least one of these clauses must match. The equivalent of OR.
```