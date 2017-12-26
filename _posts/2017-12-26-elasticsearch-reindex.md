---
layout: post
title:  "elasticsearch reindex"
crawlertitle: "elasticsearch"
summary: "how to install elasticsearch reindex and use it"
date:   2017-12-26
categories: posts
tags: 'Elasticsearch-1.7.6'
author: Becky
---
##### [Elasticsearch reindex tool]("https://github.com/allegro/elasticsearch-reindex-tool")可以很轻松的重新构建index，同样可以在clusters之前迁徙index。6.0以上的ES版本自带reindex功能

安装
* 在plugin目录下建一个reindex的目录
* 把reindex的包放进去
* 重启ES

使用
* copy数据
```
    curl -XPOST  "http://localhost:9200/old_index/old_type/_reindex/new_index/new_type"
```
* 查询copy情况
```
    curl -XPOST  "http://localhost:9200/_reindex"
```