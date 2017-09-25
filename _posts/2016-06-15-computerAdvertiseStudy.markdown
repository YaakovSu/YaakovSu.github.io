---
layout: post
title: "斯坦福大学计算广告课程学习笔记"
subtitle: ""
date: 2016-06-15
author: 苏爱马
category: 计算广告
tags: 笔记 斯坦福
finished: true
---


## 计算广告

最近看了下斯坦福大学的计算广告[课程](http://www.stanford.edu/class/msande239/)，将感觉重要的点简要做了下记录。



### 简要记录

1. Computational advertising = A principled way to find the "best match" between a user in a context and a suitable ad.

2. Advertisers are buying attention!

3. **Advertising is a form of information**
   
   Adding ads to a context is similar to the integration problem of other types of information
   
   Finding the “best ad” is often a type of information retrieval problem with multiple, possibly contradictory utility functions.

4. **Conferences where most of the action happens**

   WWW, WSDM, SIGIR, CIKM, EC

5. **搜索引擎视角**

   > 1.Ad retrieval. Match to query/context
   >
   > 2.Orderingthe ads
   >
   > 3.Pricingon a click-through

6. Ad Retrieval

   > “Exact match” The advertiser bid on that specific query a certain amount
   >
   > “Advanced match” (AM) or “Broad match” The advertiser did not bid on that specific keyword, but the query is deemed of interest to the advertiser.
   >
   > “Phrase match” query matches if sub-phrase = bids, e.g. the query <fresh red flowers> matches the bid <red flowers>

7. Types of auctions

   1. irst-price sealed-bid
   2. Second-price sealed-bid auctions (Vickrey auctions)
   3. Open Ascending-bid auctions (English auctions)\
   4. Open Descending-bid auctions (Dutch auctions)

8. 文本广告相似度计算

   1. Usually calculate similarity in a high dimensional space of features.

9. Given a phrase predict if it is “keyword”

   **feature**

   1、Linguistic features: is a noun; is a proper name; is a noun
   phrase; are all words in the phrase of the same type
   2、Capitalization: any/all/first word capitalization
   3、 Section based features:
    Hypertext – is the feature extracted from anchor text
    Title
    Meta tags
    URL
   4、 IR features: tf, idf, log(tf), log(idf), sentence length, phrase
   length, relative location in the document
   5、Query log features: log(phrase frequency), log(first/second/
   interior word frequency)

   **Conclusion**

   1、Mapping Contextual Advertising to Sponsored Search
    Extract phrases from the publisher’s web page
    Select ads using exact or advanced match on this phrase
   2、Ad selection using a single feature
   3、 Approach based on logistic regression trained on editorial
   judgments
    Editors extracting salient terms from pages
   4、 Combining the information from multiple occurrences and
   treating the phrases as single units yields best results
   5、 IR and query log features account for almost all of the signal
   6、Low precision – difficult problem

10. **When to advertise**

    **Features**
     Relevance features
     Word overlap
     Cosine similarity
     Vocabulary mismatch features
     Translation models
     Point-wise mutual information
     Chi-squared
     Ad-based features
     Bid price
     Coefficient of variation of ad scores
     Result set cohesiveness features ✓
     Result set clarity
     Entropy

11. **Predict CTR**

    *Ad features*
     Five categories considered (~80 features in total):
     Appearance: number of words in each part; word length;
    capitalization; punctuation (!#$****)
     Attention capture: action words (“buy” , “join”,…), numbers
    (prices, discounts)
     Landing page: complexity of the HTML, etc.
     Relevance: bid term in the title, body; subset of the term,…
     Reputation: short clean urls are expensive – more reputable
    domain
     One feature for the 10K most common words in title/body

     Ad group specificity:
     Entropy of the results of the bid phrase classification
     Number of bid phrases in the ad group
     Web search features:
     Query frequency
     Web page frequency

    ​

12. ***Demographic targeting***

    Important indicator of people’s interest and potential of a conversion
    Imagine you want to sell a $50K sports car. Who do you target?
    Used widely in traditional advertising:
    TV, magazines, etc. maintain very detailed statistics of their audience
    Common classic dimensions:
    Age
    Gender
    Income bracket
    Location
    Interests (“Golf enthusiast”)
    ….
    Each dimension has multiple values

    ​

13. ***Geo targeting***

    Goal: determine user location
    Home
    Current
    Often wrong 
    Inputs
    Registration data
    IP (Main source!)
    Browser default language
    Search language
    Etc …
    Lots of papers/results, but no time to discuss …

14. ***Behavioral Targeting (BT)***

    A technique used by publishers and advertisers to increase campaign effectiveness based on a given user’s historical behavior:
    Previous searches/search sessions
    Previous browsing activity
    Previous ad-clicks
    Previous conversions
    Declared demographics data
    Etc.
    Utility – everyone wins! (at least in theory  )
    Advertisers: get a more appropriate/receptive audience, increased conversion rate, better ROI
    Publishers: can ask for a premium
    Users: see more interesting ads
