---
layout: post
title:  "elasticsearch type"
crawlertitle: "elasticsearch"
summary: "What is elasticsearch type and how to use it"
date:   2017-12-26
categories: posts
tags: 'Elasticsearch-1.7.6'
author: Becky
---
##### type 是什么
使用type允许我们在一个index里存储多种类型的数据，这样就可以减少index的数量了。在使用时，向每个文档加入_type字段，在指定type搜索的时候就会被用于过滤。使用type的一个好处是，搜索一个index下的多个type和只搜索一个type相比没有额外的开销（需要合并结果的分片数量是一样的）

* 不同的type里的字段需要保持一致，一个index下的不同type里如果有两个名字相同的字段，他们的类型和配置也必须相同
* 只在某个type里存在的字段，在其他没有该字段的 type 中也会消耗资源。这意味着，只有同一个 index 的中的 type 都有类似的映射 (mapping) 时，才应该使用 type。否则，使用多个 type 可能比使用多个 index 消耗的资源更多。
* 在已有数据的情况下，type的字段名称，类型，配置不能更换

##### type操作
* 添加一个type
```
    curl -XPUT http://192.168.14.110:9200/indexname/typename/_mapping 或 curl -XPUT http://192.168.14.110:9200/indexname/_mapping/typename
    {
        "properties": {
            "name": {
            "type": "text"
            }
        }
    }
```
* 查询一个type的数据
```
    curl -XGET http://192.168.14.110:9200/indexname/typename/_search
```
* 查询一个type的结构
```
    curl -XGET http://192.168.14.110:9200/indexname/typename/_mapping
```