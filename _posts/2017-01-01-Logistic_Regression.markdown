---
layout: post
title: "逻辑回归介绍与广告算法工作中的实践"
subtitle: "逻辑回归介绍"
date: 2017-01-01
author: 苏爱马
category: 统计机器学习
tags: 最大似然 梯度下降 监督学习
finished: true
---

## 适用场景
逻辑回归虽然带有`回归`，但却是一个分类模型。通过监督学习的方法来估计模型参数，由于其易实现、可解释性强、预测时间短的优点，只需进行特征工程，就能达到不错的效果，在`计算广告`行业里受到广泛使用。

## 预测函数
逻辑回归与回归的关系是什么呢？假如我们对线性回归y=wx+b,通过训练集来训练我们的模型，也就是得到参数w，b。之后，使用训练得到的w，b来预测，此时的结果y是连续值，取值范围负无穷 - 正无穷。

那对于二分类问题，我们期望的y取值是离散二值`[0,1]`。那如果我们能用一个函数，将y=wx+b映射[0,1]，并且这个函数具有很好的可微性，我们不就可以处理二分类问题了么？！

我们找到了这个函数，这个函数就是大名鼎鼎的***Logistic函数(logistic function)***，也称为***Sigmoid函数(sigmoid function)***。


![avatar](http://52myx.cn/img/blog/lr/sigmoid.png)

sigmoid函数如下图所示：

![avatar](http://52myx.cn/img/blog/lr/sigmodimg.png)


## 损失函数与优化

构造逻辑回归的参数估计，一般使用最大似然估计法估计模型参数。
![avatar](http://52myx.cn/img/blog/lr/LRtuidao.jpeg)
这样就得到梯度上升每次迭代的更新方向。

## 为什么使用最大似然
可以证明，逻辑回归的最大似然函数是关于θ的凸函数，且有最大值。而如果使用平方损失，即：
![avatar](http://52myx.cn/img/blog/lr/pingfang.png)

我们将sigmoid函数带入上式，发现我们得到的损失函数是非凸的。也就是该函数有很多极小值，如果采用梯度下降求解的话，会导致陷入局部最优解。
![avatar](http://52myx.cn/img/blog/lr/pingfangimg.png)


***作者***

世界那么大，我就想去看看！

<i class="fa fa-github"></i>&nbsp;&nbsp;[My Github](https://github.com/YaakovSu)



