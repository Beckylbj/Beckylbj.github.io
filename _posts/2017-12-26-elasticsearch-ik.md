---
layout: post
title:  "elasticsearch ik analyzer"
crawlertitle: "elasticsearch"
summary: "how to install ik and use ik analyzer"
date:   2017-12-26
categories: posts
tags: 'Elasticsearch-1.7.6'
author: Becky
---
<h5>elasticsearch-analysis-ik 是一个中文分词插件，支持自定义词库。</h5>

* 到[github](https://github.com/medcl/elasticsearch-analysis-ik "github")，确认使用的ES版本，根据版本选定ik版本，点击下载源代码elasticsearch-analysis-ik-master.zip
* 解压文件elasticsearch-analysis-ik-master.zip
    ```
    unzip elasticsearch-analysis-ik-master.zip
    ```
* 将解压目录文件中的config/ik文件夹复制到ES安装目录config文件夹下
* 因为是源代码，此处需要使用maven打包，进入解压后的文件夹中，执行
    ```
    mvn clean package
    ```
* 将打包得到的jar文件elasticsearch-analysis-ik-1.2.8-sources.jar复制到ES安装目录的lib目录下
* 在ES的配置文件config/elasticsearch.yml中增加ik的配置
```
    index:  
        analysis:                     
            analyzer:        
            ik:  
                alias: [ik_analyzer]  
                type: org.elasticsearch.index.analysis.IkAnalyzerProvider  
            ik_max_word:  
                type: ik  
                use_smart: false  
            ik_smart:  
                type: ik  
                use_smart: true 
```
或
```
    index.analysis.analyzer.ik.type : “ik” 
```
* 重新启动ES服务

重启后做测试：
```
    curl -XPOST  "http://ip:9200/userinfo/_analyze?analyzer=ik&pretty=true&text=我是中国人" 
```
测试返回结果：
```
    {
        "tokens": [
            {
                "token": "我",
                "start_offset": 0,
                "end_offset": 1,
                "type": "CN_CHAR",
                "position": 1
            },
            {
                "token": "中国人",
                "start_offset": 2,
                "end_offset": 5,
                "type": "CN_WORD",
                "position": 2
            },
            {
                "token": "中国",
                "start_offset": 2,
                "end_offset": 4,
                "type": "CN_WORD",
                "position": 3
            },
            {
                "token": "国人",
                "start_offset": 3,
                "end_offset": 5,
                "type": "CN_WORD",
                "position": 4
            }
        ]
    }
```