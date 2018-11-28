---
layout: post
title: "在 linux（ubuntu） 下 安装 LibSVM"
subtitle: ""
date: 2014-12-24
author: 苏爱马
category: 工具
tags: linux libsvm
finished: true
---

在安装LibSVM前需要先装 python 和 gnuplot

linux 一般都自带了python2.7，所以python的安装不再赘述

在 ubuntu 下安装 gnuplot 不能直接 sudo apt-get install gnuplot，因为预编译的gnuplot不能识别ubuntu的图形界面，所以必须先运行这句：



[plain] view plaincopy

sudo apt-get install libx11-dev   

然后从下载 gnuplot的源代码：





[plain] view plaincopy

wget http://nchc.dl.sourceforge.net/project/gnuplot/gnuplot/4.6.rc1/gnuplot-4.6.rc1.tar.gz  

将其解压缩，进入解压后的目录 编译 ，安装：





[plain] view plaincopy

tar xzvf gnuplot-4.6.rc1.tar.gz  
cd gnuplot-4.6.rc1  
./configure  
make  
sudo make install  


安装 LibSVM：



[plain] view plaincopy

wget http://www.csie.ntu.edu.tw/~cjlin/cgi-bin/libsvm.cgi?+http://www.csie.ntu.edu.tw/~cjlin/libsvm+tar.gz  

下载完成后解压，我把libsvm文件夹放到了 /usr/bin 目录下，然后在tools文件夹下找到 easy.py 和 grid.py 两个文件。把其中 gnuplot 的路径设置好。注意gnuplot的pathname不是解压的那个目录，而是要用 which gnuplot 命令来找出。我安装完后gnuplot的路径是 /usr/local/bin/gnuplot

最后执行在libsvm的文件夹下执行make命令，在子目录python下执行make命令。

至此 libsvm的安装完成！



***作者***

世界那么大，我就想去看看！

<i class="fa fa-github"></i>&nbsp;&nbsp;[My Github](https://github.com/YaakovSu)



