---
layout: post
title: "ubuntu使用scrapy爬取微信评论信息"
subtitle: ""
date: 2015-12-07
author: 苏爱马
category: 工具
tags: 爬虫 微信
finished: true
---

由于微信的评论数据只能使用微信客户端查看。所以，我们使用抓包工具来获取评论的url，然后使用scrapy进行爬取。其中的fiddler



（1）ubuntu安装scrapy

1、python版本必须使用2.7。因为目前scrapy还不能支持python3.x，需要修改源码。

2、安装依赖包：lxml，OpenSSL（一般默认已安装，测试方法，在python界面输入 import lxml;  import OpenSSL）

3、sudo apt-get install python-dev

4、sudo apt-get install libevent-dev

5、接下来就是安装pip了，执行：apt-get install python-pip

6、最后，也就是最重要的，安装Scrapy。执行：pip install Scrapy

（2）安装抓包工具Fiddler，并配置

1、安装过程：



Linux(Ubuntu)环境下使用Fiddler
自己的开发环境是Ubuntu, 对于很多优秀的软件但是又没有Linux版本这件事，还是有点遗憾的。比如最近遇到一个问题，在分析某个网站的请求路径和cookie时就遇到了问题。本来Chome浏览器自带的开发者工具对我这种后台开发程序来说足够了，但是有个场景问题难住了：当网页有链接打开一个新的页面，而且这个新打开的页面是在另一个标签页中打开，那么原来页面的控制台不能记录这个请求数据。我在google找了半天没找到好的办法，有个不是办法的办法是在chrome地址栏里输入chrome://net-internals/#events，但是用过就知道太不好用了。一般在这个时候才会想起Windows的好来，起码可以用Fiddler啊。哦，对，好像有个什么东西，不是可以跨平台跑.NET的程序应用吗，那个是谁，哦，是Mono。本篇文章介绍下在Linux环境下如何使用Fiddler。

首先，你要有个Mono环境，在Ubuntu环境下安装很简单，输入：

sudo apt-get install mono-complete
下载一个最新的Fiddler for Mono版本，我写这篇文章时最新版本是这个。下载完成后，解压到你的习惯放置的随便一个目录里。然后cd到目录下，运行：

tony@tony:~/devs/fiddler$ mono Fiddler.exe
此时，安装fiddler完毕。

2、Fiddler配置



配置Fiddler,  允许"远程连接"


打开Fiddler,     Tools-> Fiddler Options 。  （配置完后记得要重启Fiddler）.

选中"Decrpt HTTPS traffic",    Fiddler就可以截获HTTPS请求

选中"Allow remote computers to connect".  是允许别的机器把HTTP/HTTPS请求发送到Fiddler上来









获取Fiddler所在机器的IP地址
这个简单吧。   我Fidder所在的机器地址是: 192.168.1.104



IPhone上安装Fiddler证书
这一步是为了让Fiddler能捕获HTTPS请求。 如果你只需要截获HTTP请求， 可以忽略这一步

1. 首先要知道Fiddler所在的机器的IP地址：　假如我安装了Fiddler的机器的IP地址是:192.168.1.104

2. 打开IPhone 的Safari, 访问  http://192.168.1.104:8888， 点"FiddlerRoot certificate" 然后安装证书









IPhone上配置Fiddler为代理
 打开IPhone,  找到你的网络连接， 打开HTTP代理， 输入Fiddler所在机器的IP地址(比如:192.168.1.104) 以及Fiddler的端口号8888





大功告成，开始抓包
现在IPhone上的应用（比如Safari, Firefox, Itunes, App Store）发出的HTTP/HTTPS都可以被Fiddler获取。 

实例：　打开Safari，　　

1. 输入http://www.cnblogs.com/tankxiao.  看看Fiddler能否捕获。

2.  输入https://dynamic.12306.cn/otsweb/   看看Fiddler能否捕获。

是不是HTTP和HTTPS都截获到了？？？？，  你不但能截获， 还可以下断点，修改Request, 修改Response, Do what you want. 



用完了， 记得把IPhone上的Fiddler代理关闭， 以免IPhone上不了网。



只能捕获HTTP,而不能捕获HTTPS的解决办法
有时候会发现， Fiddler 只能捕获IPhone发出得HTTP请求， 而不能捕获HTTPS请求， 原因可能是证书没有安装好。 解决办法是：

1. 先把IPhone上所有的Fiddler证书删除 (拿出IPhone， 点”设置“->“通用”->"描述文件")

2. 安装上面的方法，重新安装Fiddler证书



Fiddler捕获其他手机或者平板
方法类似

mac的配置方法参看http://www.cnblogs.com/TankXiao/archive/2013/04/18/3027971.html



（3）创建scrapy爬虫

1.新建项目（Project）

在空目录下按住Shift键右击，选择“在此处打开命令窗口”，输入一下命令：



[plain] view plaincopy

scrapy startproject tutorial  

其中，tutorial为项目名称。



可以看到将会创建一个tutorial文件夹，目录结构如下：



[plain] view plaincopy

tutorial/  
    scrapy.cfg  
    tutorial/  
        __init__.py  
        items.py  
        pipelines.py  
        settings.py  
        spiders/  
            __init__.py  
            ...  






下面来简单介绍一下各个文件的作用：

scrapy.cfg：项目的配置文件
tutorial/：项目的Python模块，将会从这里引用代码
tutorial/items.py：项目的items文件
tutorial/pipelines.py：项目的pipelines文件
tutorial/settings.py：项目的设置文件
tutorial/spiders/：存储爬虫的目录


2.明确目标（Item）

在Scrapy中，items是用来加载抓取内容的容器，有点像Python中的Dic，也就是字典，但是提供了一些额外的保护减少错误。

一般来说，item可以用scrapy.item.Item类来创建，并且用scrapy.item.Field对象来定义属性（可以理解成类似于ORM的映射关系）。

接下来，我们开始来构建item模型（model）。

首先，我们想要的内容有：

名称（name）
链接（url）
描述（description）


修改tutorial目录下的items.py文件，在原本的class后面添加我们自己的class。

因为要抓dmoz.org网站的内容，所以我们可以将其命名为DmozItem：



[python] view plaincopy

# Define here the models for your scraped items  
#  
# See documentation in:  
# http://doc.scrapy.org/en/latest/topics/items.html  
  
from scrapy.item import Item, Field  
  
class TutorialItem(Item):  
    # define the fields for your item here like:  
    # name = Field()  
    pass  
  
class DmozItem(Item):  
    title = Field()  
    link = Field()  
    desc = Field()  




刚开始看起来可能会有些看不懂，但是定义这些item能让你用其他组件的时候知道你的 items到底是什么。

可以把Item简单的理解成封装好的类对象。



3.制作爬虫（Spider）

制作爬虫，总体分两步：先爬再取。

也就是说，首先你要获取整个网页的所有内容，然后再取出其中对你有用的部分。

3.1爬

Spider是用户自己编写的类，用来从一个域（或域组）中抓取信息。

他们定义了用于下载的URL列表、跟踪链接的方案、解析网页内容的方式，以此来提取items。

要建立一个Spider，你必须用scrapy.spider.BaseSpider创建一个子类，并确定三个强制的属性：

name：爬虫的识别名称，必须是唯一的，在不同的爬虫中你必须定义不同的名字。
start_urls：爬取的URL列表。爬虫从这里开始抓取数据，所以，第一次下载的数据将会从这些urls开始。其他子URL将会从这些起始URL中继承性生成。
parse()：解析的方法，调用的时候传入从每一个URL传回的Response对象作为唯一参数，负责解析并匹配抓取的数据(解析为item)，跟踪更多的URL。


这里可以参考宽度爬虫教程中提及的思想来帮助理解，教程传送：[Java] 知乎下巴第5集：使用HttpClient工具包和宽度爬虫。

也就是把Url存储下来并依此为起点逐步扩散开去，抓取所有符合条件的网页Url存储起来继续爬取。





下面我们来写第一只爬虫，命名为dmoz_spider.py，保存在tutorial\spiders目录下。

dmoz_spider.py代码如下：



[python] view plaincopy

from scrapy.spider import Spider  
  
class DmozSpider(Spider):  
    name = "dmoz"  
    allowed_domains = ["dmoz.org"]  
    start_urls = [  
        "http://www.dmoz.org/Computers/Programming/Languages/Python/Books/",  
        "http://www.dmoz.org/Computers/Programming/Languages/Python/Resources/"  
    ]  
  
    def parse(self, response):  
        filename = response.url.split("/")[-2]  
        open(filename, 'wb').write(response.body)  
allow_domains是搜索的域名范围，也就是爬虫的约束区域，规定爬虫只爬取这个域名下的网页。

从parse函数可以看出，将链接的最后两个地址取出作为文件名进行存储。

然后运行一下看看，在tutorial目录下按住shift右击，在此处打开命令窗口，输入：

[plain] view plaincopy

scrapy crawl dmoz  
在爬取微信评论是，需要修改dmoz_spider.py中的代码

[python] view plaincopy

import scrapy  
  
class DmozSpider(scrapy.Spider):  
    name = "dmoz"  
    allowed_domains = ["mp.weixin.qq.com"]  
    start_urls=[]  
    for line in open("/home/SuNoob/crawel/myCrawel/pagelist"):  
        if line.startswith("https://mp.weixin.qq.com/mp/appmsg_comment?action=getcomment"):  
            start_urls.append(line)  
  
    def parse(self, response):  
        filename = response.url.split("/")[-1].split("&")[2].split("=")[1] + '.html'  
        with open(filename, 'wb') as f:  
            f.write(response.body)  


然后就可以根据之前抓到的url链接进行爬取了。






***作者***

世界那么大，我就想去看看！

<i class="fa fa-github"></i>&nbsp;&nbsp;[My Github](https://github.com/YaakovSu)



