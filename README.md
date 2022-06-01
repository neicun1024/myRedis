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

1. 采用Docker安装，准备一个YAML文件：
```yml
version: '3'
services:
    redis: 
        image: daocloud.io/library/redis:5.0.7
        restart: always
        container_name: redis
        environment: 
            - TZ=Asia/Shanghai
        ports:
            - 6379:6379
```
2. 创建`docker-compose.yml`文件，并写入上面的配置
3. 执行`docker-compose up -d`，如果出现错误：`docker: Error response from daemon: Ports are not available: listen tcp 0.0.0.0:4449: bind: An attempt was made to access a socket in a way forbidden by its access permissions.`就在命令行输入`netcfg -d`并重启电脑
4. 执行`docker ps`查看当前启动的docker容器

### 2.2 连接Redis

1. 执行`docker exec -it 99 bash`来进入容器，其中`99`表示该容器的标志符，就是`CONTAINER ID`的前两位
2. 使用`redis-cli`连接Redis
3. 可以简单输入两条命令`set name zhangsan`和`get name`，可以看到`'zhangsan'`被存入了Redis数据库
4. 使用图形化界面连接Redis，从[GitHub](https://github.com/lework/RedisDesktopManager-Windows/releases)下载并安装，连接到Redis服务器，可以看到db0中有`'zhangsan'`


# 三. Redis常用命令

## 3.1 Redis存储数据的结构

常用的5种数据结构
- key-string：一个key对应一个值，是最常用的，一般用于存储一个值
- key-hash：一个key对应一个map，存储一个对象数据的
- key-list：一个key对应一个列表，使用list结构实现栈和队列结构
- key-set：一个key对应一个集合，提供交集、差集和并集的操作
- key-zset：一个key对应一个有序的集合，适合排行榜，积分存储等操作

![20220601161158](https://raw.githubusercontent.com/neicun1024/PicBed/main/images_for_markdown/20220601161158.png)

另外三种数据结构
- HyperLogLog：用于计算近似值
- GEO：用于存储地理位置，即经纬度
- BIT：一般存储的也是一个字符串，存储的是一个byte[]

## 3.2 key-string常用命令