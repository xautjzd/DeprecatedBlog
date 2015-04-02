---
layout: post
title: "我的第一篇博客"
date: 2013-07-18 12:42
comments: true
categories: [Octopress, Thinking]
---
几个月前看过Ruby基本语法，也无意中接触了Octopress，便想在GitHub pages上采用Octopress搭建一个属于自己的博客，照着官网提示开始动手实施，不过最后以失败告终。后又忙于其他工作，此事便搁浅。直至最近得空，便又开始着手此事。搭建博客工作再一次展开。
详细搭建过程官方文档写的相当详细，这里不再赘述，请参考：
[官网](octopress.org/docs/setup)  
下面只说我搭建过程中遇到的难题：
我每次都是运行rake deploy时出现问题，也就是博客无法push到github的repository中。
每次都是![rejected] master->master (no-fast-forward)
最后网上找了不少资料，然后自己也细细思考了一番，最后终得以解决。方法如下：
转到deploy目录下，执行$git pull，然后再执行git push origin master即可。
