---
layout: post
title: "Hexo博客搭建系列教程（三）域名绑定"
subtitle: "给自己的小博客一个域名吧"
date: 2016-04-22
author: Yaakov Su
category: 技术
tags: hexo 系统
finished: true
---



##  购买域名与设置DNS
博客搭建好了，但是感觉直接使用`yaakovsu.github.io`作为访问路径好丑啊，所以，我们就需要买个域名，顶级域名使用`.com`, `.cn`, `.me`都可以，只不过是价格高低的问题。推荐的话，感觉还是首选Goddady，为啥呢？我就说一点：支持支付宝付款=-=。当然价格上也不高，60块￥左右，而且信誉较好。

购买的过程就不说了。。。。。

之后，由于我们需要提供国内的访问服务，所以，我们最好选择国内的dns服务商户来提供域名解析服务，我选择的是[dnspod](http://dnspod.cn/)。在[dnspod](http://dnspod.cn/)上注册帐号，在上面添加网址（例如：`yaakovary.com`），设置域名的映射关系：

![dnspod](http://yaakovary.com/img/blog/dnspod.png)

其中，主机记录描述访问你网址的前缀`www`, `@`。记录类型选择`A`，则在记录值里面填写`yourname.github.io`的ip地址。记录值选择`CNAME`，则记录值里填写`yourname.github.io`。什么？你不知道如何获取`yourname.github.io`的ip地址....=-=。方法就是在命令行里，`ping`  你的repository `yourname.github.io`。



同时，请记下`dnspod`提供给你的两个域名解析服务器，`f1g1ns1.dnspod.net`和`f1g1ns2.dnspod.net`。

之后登录[GoDaddy](https://sg.godaddy.com/zh/)，登陆自己的账户，在管理域名服务器上，设置域名服务器为`f1g1ns1.dnspod.net`和`f1g1ns2.dnspod.net`。



##  域名绑定

在设置好了DNS之后，还需要将你`yourname.github.io`与该域名绑定。

1. 首先，打开github仓库，在博客仓库目录下新增文件，命名为CNAME，并且写入购买的域名。

   ![cname](http://yaakovary.com/img/blog/CNAME.png)

   ​

2. 更改博客仓库的**_config.yml**配置，设置url为购买域名地址

3. 保存配置后，点击仓库的Settings，如果出现链接地址是蓝色的，那么说明博客跟域名已经关联好了，等待几分钟就可以通过自己购买的域名进行访问。

   ![ok](http://yaakovary.com/img/blog/ok.png)



好了，现在你就可以真正的拥有一个Blog个，但是，如果我还想能够让其他人评论我的博客，还想查看博客的访问量，还想统计网站的访问者信息，还想提供分享功能。。。。。。太多了，该怎么办呢？请看我的下一篇Blog，给网站加入功能。



