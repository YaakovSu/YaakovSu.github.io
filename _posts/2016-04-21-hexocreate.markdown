---
layout: post
title: "Hexo博客搭建系列教程（二）"
subtitle: "Hexo搭建"
date: 2016-04-21
author: Yaakov Su
category: 技术
tags: Hexo 系统
finished: true
---



### 注意

本节的教程只针对`Windows`用户，`Mac`和`Linux`用户请自行查看hexo的[官方文档](https://hexo.io/zh-cn/docs/)。

##  安装Git
下载[msysgit](http://code.google.com/p/msysgit/)，并执行安装。Windows下`git`的配置过程参看[Windows下Git安装指南](http://www.cnblogs.com/zhcncn/p/3787849.html)。

## 安装Node.js
Windows下面安装Node.js，仅需下载[安装程序](https://nodejs.org/en/)，点击安装就好了。



##  安装hexo

在电脑任意位置，右键选择`Git Bash`，输入如下命令：

```shell
npm install -g hexo
```

##  创建hexo文件夹

在安装完hexo后，在你的计算机上建立hexo的文件夹（例如`D:\hexo`），在`D:\hexo`中右键选择`Git Bash`，执行如下命令：

```shell
hexo init
```



## 安装依赖包

安装相关依赖的方法为：

```shell
npm install
```



依赖安装好了以后，你可以在本地查看搭建的hexo博客了=-=，在hexo目录下（例如`D:\hexo`），右键选择`Git Bash`，执行如下命令：

```shell
hexo generate
hexo server
```

然后在浏览器输入`localhost:4000`就可以看到部署的网站了。不过博客是在本地的，只能你自己看到。下面要做的就是把博客部署到`Github`上。

## 创建repository

我默认大家都有`Github`的帐号=-=，所以注册`Github`帐号的过程就不写了。创建一个以你github名字命名的`repository`，例如，我的名字叫`YaakovSu`，所以我建的repository的名字为`YaakovSu.github.io`。

![repository](http://yaakovary.com/img/blog/createRepository.png)

