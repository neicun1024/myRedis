# 一. Redis介绍

## 1.1 引言

>1. 由于用户量增大，请求数量也随之增大，数据压力过大
>2. 多台服务器之间，数据不同步
>3. 多态服务器之间的锁，不存在互斥性

![20220530204310](https://raw.githubusercontent.com/neicun1024/PicBed/main/images_for_markdown/20220530204310.png)

## 1.2 NoSQL

NoSQL（Not Only SQL）：非关系数据库
1. key-value：Redis。。。
2. 文档型：ElasticSearch，Solr，MongoDB。。。
3. 面向列：Hbase，Cassandra。。。
4. 图形化：Neo4j。。。

除了非关系型数据库都是关系型数据库。

NoSQL只是一种概念，泛指非关系型数据库，和关系型数据库做一个区分

## 1.3 Redis介绍

有一位意大利人，在开发一款LLOOGG的统计页面，因为MySQL的性能不好，就自己研发了一款非关系型数据库，并命名为Redis。

- Redis（Remote Dictionary Server）即远程字典服务
- Redis是由C语言编写的，是一款基于key-value的NoSQL
- 基于内存存储数据的，提供多种持久化机制，性能可以达到110000次/s读取数据以及81000次/s写入数据
- 提供主从，哨兵以及集群的搭建方式，可以更方便地横向扩展和垂直扩展

# 二. Redis安装

## 2.1  安装Redis

采用Docker安装，准备一个YAML文件：
```yml
version: '3.1'
services:
    redis: 
        image:
```