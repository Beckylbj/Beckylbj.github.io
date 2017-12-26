---
layout: post
title:  "elasticsearch index"
crawlertitle: "elasticsearch"
summary: "What is elasticsearch index and how to use it"
date:   2017-12-26
categories: posts
tags: 'Elasticsearch-1.7.6'
author: Becky
---
##### Index 是什么
假如依照关系型数据库做一个比喻，index就像关系型数据库里的database，type就像database里的table。但这并不正确

Index存储在多个分片中，其中每一个分片都是一个独立的Lucene Index。每个Lucene Index都需要消耗一些磁盘，内存和文档描述符。因此，一个大的index比多个小index效率更高：Lucene Index的固定开销被摊分到更多文档上了

当在考虑是创建index还是type的时候可以问自己以下几个问题
+ 你的文档的映射是否相似？如果不相似，使用多个index
+ 每个type是否都有足够多的文档，如果有，可以使用多个index，如果必要，可以把分片数量设小一点
+ 如果文档不够多，可以考虑放到一个index的多个type甚至一个type里

##### index操作
* 添加一个index
```
    curl -XPUT http://192.168.14.110:9200/indexname
```
* 删除一个index
```
    curl -XDELETE http://192.168.14.110:9200/indexname
```
* 查询一个index的数据
```
    curl -XGET http://192.168.14.110:9200/_search
```
* 查询一个index的结构
```
    curl -XGET http://192.168.14.110:9200/_mapping
```