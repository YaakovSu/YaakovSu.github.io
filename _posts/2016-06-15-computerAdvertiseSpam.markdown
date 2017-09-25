---
layout: post
title: "反作弊初期一些参考资料"
subtitle: ""
date: 2016-06-15
author: 苏爱马
category: 计算广告
tags: 反作弊 资料
finished: true
---


# 记录

* 判断文件编码，使用`cpdetector_1.0.10_binary`中的jar进行，参考了[java课程设计例子](http://www.cnblogs.com/java0721/archive/2012/07/21/2602963.html)。


* 日志文件里面含有大量`ASCII 控制字符`，例如，`SOH`, `NUL`等，ASCII`控制字符`和ASCII`可显示字符`的相关对应表见[ASCII控制字符和ASCII可显示字符](http://www.cnblogs.com/kakafra/archive/2013/01/07/2850099.html)。`ADirect`给的数据的用法应该是如何处理这些不可见的字符，即`ASCII 控制字符`，可在`bing`中搜索`java 不可见字符 ascii`。
* `ADirect`用的是类似`Thrift`的`Avro`来进行数据的序列化和反序列化。`Avro`的`Jar`的下载路径为[avro](http://www.trieuvan.com/apache/avro/avro-1.7.7/java/)。java读写avro的例子为[例子](http://www.knowsky.com/889897.html)。
* `Hive`使用`AVRO`，读取`HDFS`多级子目录中的数据，需要在执行creat表之前先执行两个命令：
  * set hive.mapred.supports.subdirectories=true;
  * set mapreduce.input.fileinputformat.input.dir.recursive=true;参考 [多级目录](http://www.itnose.net/detail/6491934.html)。
  * 参考资料[在Hive中使用Avro](http://www.cnblogs.com/xd502djj/p/4089644.html)。
  * `ubuntu`安装`hive`[Ubuntu + hadoop2.6.0下安装Hive](http://www.cnblogs.com/hanyefeng/p/5144500.html)。
  * [hive安装报Unable to instantiate org.apache.hadoop.hive](http://my.oschina.net/AlbertHa/blog/339022)。
  * [Hive几种建表方式](http://blog.csdn.net/xiao_jun_0820/article/details/32328755)。
  * [Hadoop常用命令](http://blog.chinaunix.net/uid-10915175-id-3258669.html)。
  * `Hive`查询结果的三种导出形式[参考](http://www.aboutyun.com/thread-7439-1-1.html)。
  * 使用`Java`调用`Hive`在启动service服务的时候报错，原因是已经用hive server2代替了hiveserver。具体[参考](http://my.oschina.net/zc741520/blog/496877)。
  * ​