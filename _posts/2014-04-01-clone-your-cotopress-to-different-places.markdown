---
layout: post
title: "随时随地用Octopress写博客"
date: 2014-04-01 11:00
comments: true
categories: Octopress
---

![](/images/20140401octopress.jpg)

[Octopress](http://octopress.org/)所依赖的环境是Ruby和Git,所以要使用它写博客，必须先确保目标机器上已经安装Ruby和Git。有时候可能需要在新的环境中创作，那么得进行以下的一些操作了。在讲操作前先简要介绍下Octopress如何工作。

## Octopress是怎么工作的?

Octopress默认有两个分支，即master和source。source分支主要存储用于生成博客的源文件，而master分支则主要包含生成后的博客。master分支存储在_deploy文件夹中，之所以以下划线命名，是因为在执行`git push origin source`时，下划线开头的文件夹会被忽略掉。

当然，也可以创建自己的分支，但master分支一般主要用于存储生成后的博客，而博客源文件则可以自己新建分支存储。我目前在原有的基础上新建了newtheme分支，用于更改主题后的博客源码存储，以前的源码存储在source分支。

## 创建本地Octopress库

在新环境中写作时，需要进行以下几个步骤：

<!-- more -->

### 克隆博客到新机器

首先，需要克隆source分支到新机器上:

```
$ git clone -b source git@github.com:username/usename.github.com.git Octopress
```

### 设置GitHub Repository

克隆source到本地后，默认没有_deploy目录，所以还需要创建_deploy，进行git init操作，同时也要设置remote respository。这几个步骤可以通过手动完成，但作为使用者，当然是操作越简单越好，能够自动化完成就自动化。这里Octopress提供了一个自动化完成这几个步骤的脚本，执行它即可。

```
$ rake setup_github_pages
```
在出现的提示符后输入自己对应的remote repository即可。

以上操作即可完成remote repository的设置，另一种方法是直接克隆master分支到本地：

```
$ cd Octopress
$ git clone git@github.com:username/username.github.com.git _deploy
```

接下来就是安心写作的时刻了。


