---
layout: post
title:  "elasticsearch index alias"
crawlertitle: "elasticsearch"
summary: "how to use index alias"
date:   2017-12-26
categories: posts
tags: 'Elasticsearch-1.7.6'
author: Becky
---
##### Elasticsearch的别名
###### index aliases的API允许我们为一个index指定别名。一个别名能够被映射到多个index中，当指定了index对应已经有其它index对应的别名之后，别名可以自动扩展到多个index。一个别名能够关联上一个过滤器，当搜索和路由的时候能够自动使用这个过滤器。

* 查询别名
```
    curl -XGET 'http://localhost:9200/index/_alias'
```
返回结果
```
    {
        "index": {
            "aliases": {}
        }
    }
```

* 创建index别名
```
    curl -XPOST 'http://localhost:9200/index/_alias/index_alias'
```
或
```
    curl -XPOST 'http://localhost:9200/_aliases'
    {  
        "actions" : [  
            { "add" : { "index" : "test1","alias" : "alias1" } }  
        ]  
    }
```
成功返回
```
    {
        "acknowledged": true
    }
```

* 删除index别名
```
    
    {  
        "actions" : [  
            { "remove" : { "index" : "testalias","alias" : "testalias_v2" } }  
        ]  
    }
```
成功返回
```
    {
        "acknowledged": true
    }
```