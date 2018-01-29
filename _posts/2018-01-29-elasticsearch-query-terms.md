---
layout: post
title:  "elasticsearch common terms query(常用术语查询)"
crawlertitle: "elasticsearch"
summary: "How to query in elasticsearch"
date:   2018-01-29
categories: posts
tags: 'Elasticsearch-1.7.6'
author: Becky
---
<h5>common terms query 是stopword一个替代方案. 它可以提升精确度, 还不会牺牲性能.</h5>


* 第一步, 先搜索更重要的term, 它们是低频词, 对相关性的影响更大.

* 第二步, 再对高频词执行第二次搜索. 但是它不对所有匹配的文档打分, 只对第一步中匹配的文档打分. 这样的话, 高频词也可以提升结果的相关性, 同时还不会增加很多负载.如果query里面的term全是高频词,那么query会按照 AND queyr来执行(默认是or).


* 怎么样才算高频词呢? 

```
    cutoff_frequency 来控制, 哪些是高频词, 哪些是低频词. cutoff_frequency <= 1的时候,代表一个比率, 如果大于1, 代表一个绝对值. cutoff_frequency 是单个shard级别计算的.

    最有趣的是, stopword是自动的, 在一个视频网站, “video”这个term可能就自动变成了stopword(其实也就是指高频词)
```