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
* 只在某个type里存在的字段，在其他没有该字段

但是，这也是有限制的：

不同 type 里的字段需要保持一致。例如，一个 index 下的不同 type 里有两个名字相同的字段，他们的类型（string, date 等等）和配置也必须相同。
只在某个 type 里存在的字段，在其他没有该字段的 type 中也会消耗资源。这是 Lucene Index 带来的常见问题：它不喜欢稀疏。由于连续文档之间的差异太大，稀疏的 posting list 的压缩效率不高。这个问题在 doc value 上更为严重：为了提高速度，doc value 通常会为每个文档预留一个固定大小的空间，以便文档可以被高速检索。这意味着，如果 Lucene 确定它需要一个字节来存储某个数字类型的字段，它同样会给没有这个字段的文档预留一个字节。未来版本的 ES 会在这方面做一些改进，但是我仍然建议你在建模的时候尽量避免稀疏。[1]
得分是由 index 内的统计数据来决定的。也就是说，一个 type 中的文档会影响另一个 type 中的文档的得分。
这意味着，只有同一个 index 的中的 type 都有类似的映射 (mapping) 时，才应该使用 type。否则，使用多个 type 可能比使用多个 index 消耗的资源更多。