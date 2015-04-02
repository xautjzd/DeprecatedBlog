---
layout: post
title: "查看网站所用Web服务器类型"
date: 2013-09-04 16:43
comments: true
categories: [Thinking,Linux]
---
学习Rails的Layout过程中，其中有提到curl，所以便简单的看了下curl的功能。虽说以前学习Shell的过程中也看到过curl,不过没怎么用过，只知道和wget功能类似，只是wget是将请求的web资源下载到本地，而curl则是在shell中显示，至于有什么其他功能也便不清楚。但是今天发现curl其实还可以用来查看website所用的web服务器类型，通过`curl -I url-you-want-to-lookup`命令查看即可。以下是我查看ruby-china的一个截图：
![](http://pic.yupoo.com/xautjzd/D8xXpw6z/medish.jpg)

从中可以发现ruby-china采用的是nginx服务器。至于curl其他的功能慢慢再发掘吧。

