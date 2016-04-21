---
layout: post
title: "Hexo博客搭建系列教程（三）"
subtitle: "给自己的小博客一个域名"
date: 2016-04-21
author: Yaakov Su
category: 技术
tags: hexo 系统
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



## 部署

编辑`D:\hexo`下面的`_config.yml`文件，`repository`换成自己的，如果有自己的域名了，可以将`url`换成自己的域名：

```json
url: http://yaakovary.com
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:

deploy:
  type: git
  repository: https://github.com/YaakovSu/YaakovSu.github.io.git
  branch: master
```

注意：针对hexo3.0版本，这里的type要写成`git`，若是2.x版本，type写为`github`。

之后执行如下命令，完成部署：

```shell
hexo generate
hexo deploy
```

注意：如果修改了本地文件，需要`hexo generate`后才保存。若是需要设置ssh，请查看[官方教程](https://help.github.com/articles/generating-an-ssh-key/)。

上述步骤都进行完了以后，在浏览器里输出`yaakovSu.github.io`就能看到你自己的网站了。是不是感觉直接输入这个地址有点丑啊，如果想拥有自己的域名，请移步