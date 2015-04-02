---
layout: post
title: "Ruby中symbol与string的区别"
date: 2013-08-18 20:50
comments: true
categories: [Ruby]
---
记得当初学习Ruby基本语法时，还为Symbol与String的异同纠结了好久，后来经过一段时间的摸索，大致有了了解，但让我给他人解释，这点我还是办不到。但是今天看到了一篇[博文](http://www.gaurishsharma.com/2013/04/understanding-differences-between-symbols-strings-in-ruby.html),让我彻底明白他们的区别。

### symbol定义

Symbol其实就是string加上前缀：。

### 二者异同点

其实Symbol与String本质相同，是string 的两种不同呈现方式。由于受SmallTalk影响，Ruby一切皆对象。所以每次给string赋值，`name="xautjzd"`其实都是在内存中创建一个新对象。每次创建的对象的object_id都不相同。

而symbol则不同，symbol创建一次即可。以后所有的操作都是指向先前创建的对象。所以object_id相同。

不同点大致有三：
1. symbol为常量，值不能改变。
2. 多次使用同一个symbol,object_id相同，而多次使用string,每个对象有不同的object_id。
3. String的方法,eg:#upcase,#split不能用于Symbol。

### 参考网址

http://www.gaurishsharma.com/2013/04/understanding-differences-between-symbols-strings-in-ruby.html(http://www.gaurishsharma.com/2013/04/understanding-differences-between-symbols-strings-in-ruby.html)


