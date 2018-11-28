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

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

## 适用场景
逻辑回归虽然带有`回归`，但却是一个分类模型。通过监督学习的方法来估计模型参数，由于其易实现、可解释性强、预测时间短的优点，只需进行特征工程，就能达到不错的效果，在`计算广告`行业里受到广泛使用。

## 预测函数
逻辑回归与回归的关系是什么呢？假如我们对线性回归y=wx+b,通过训练集来训练我们的模型，也就是得到参数w，b。之后，使用训练得到的w，b来预测，此时的结果y是连续值，取值范围[$-\infty$,$+\infty$]。

那对于二分类问题，我们期望的y取值是离散二值`[0,1]`。那如果我们能用一个函数，将y=wx+b映射[0,1]，并且这个函数具有很好的可微性，我们不就可以处理二分类问题了么？！

我们找到了这个函数，这个函数就是大名鼎鼎的***Logistic函数(logistic function)***，也称为***Sigmoid函数(sigmoid function)***。

$$g(z)=\frac{1}{1+e^{-z}}$$
<img src="http://chart.googleapis.com/chart?cht=tx&chl= g(z)=\frac{1}{1+e^{-z}}" style="border:none;">

![avatar](http://52myx.cn/img/blog/lr/LRtuidao.jpeg)

## 损失函数与优化
建个Blog网站不告诉你们怎么用，这怎么能行呢？

网站主界面包括个人的一些说明，还有[时间记录](http://52myx.cn/archive/)，[类别记录](http://yaakovary.com/category/)，[标签记录](http://yaakovary.com/tags/)，[其他工作](http://yaakovary.com/contact/)，[关于我](http://yaakovary.com/about/)，五个子页面。大家如果有什么问题或则建议可以通过点击下面facebook，twitter，weibo，email的图标来联系我，同时欢迎大家follow我的Github，disqus。

![index-page](http://52myx.cn/img/blog/lr/LRtuidao.jpeg)

 `时间记录` 页面按照时间顺序来记录我写的Blog，大家可以通过点击下面的`Yaakov Su`  返回主页面:
![archive-page](http://yaakovary.com/img/blog/archive.png)

`类别记录` 页面按照blog的类别来记录，点击下面的`Yaakov Su`  返回主页面:  
![category-page](http://yaakovary.com/img/blog/category.png)

`标签记录` 页面按照blog的标签来记录，点击下面的`Yaakov Su`  返回主页面:  
![tags-page](http://yaakovary.com/img/blog/tags.png)

`其他工作` 里记录了一些我做过的其他小项目，欢迎大家去看看:  
![contact-page](http://yaakovary.com/img/blog/contact.png)

`关于我` 页面记录了我建这个小网站的背景，还有我的一些基本信息:  
![about-page](http://yaakovary.com/img/blog/about.png)

当然 `404` 页面说明你访问的页面我还没写:  
![404-page](http://yaakovary.com/img/blog/404.png)

## 评论

如果大家对Blog有什么疑问，欢迎大家进行评论。
![question-page](http://52myx.cn/img/blog/question.png)

## 作者

世界那么大，我就想去看看！

<i class="fa fa-twitter"></i>&nbsp;&nbsp;[Twitter](https://twitter.com/doG__uS)



