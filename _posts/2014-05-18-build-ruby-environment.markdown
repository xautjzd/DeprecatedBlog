---
layout: post
title: "Ruby环境的搭建"
date: 2014-05-18 11:50
comments: true
categories: [Ruby]
---

![](/images/20140518.jpg)

## Ruby简介

第一次听到Ruby这个名词，可能会比较陌生，进而产生畏惧，毕竟在中国这片区域普及率还不是很高，但在世界范围内还是有不错的影响力，如果有所质疑，可以参考[TIOBE](http://www.tiobe.com/index.php/content/paperinfo/tpci/index.html)上Ruby的排名情况，进几年一直在前10左右徘徊。到目前为止，大家可能只了解到Ruby是一门编程语言，具体还未做了解，那这里引用[Ruby官网](https://www.ruby-lang.org/en/)的解释，供大家参考：

>Ruby is a dynamic, open source programming language with a focus on simplicity and productivity. It has an elegant syntax that is natural to read and easy to write.

用再多的语言描述都略显苍白，只有身临其中把玩一番才能有所体会，而且这种感触才最直观，最有说服力。这里，贴出一个网址，便可在浏览器中体验Ruby之美：

> [http://tryruby.org/levels/1/challenges/0](http://tryruby.org/levels/1/challenges/0)

请感受它的魅力所在吧。

<!-- more -->

## 操作系统

Ruby是跨平台的语言，所以Windows、Linux和Mac OS X都可安装，但不建议在Windows上搭建环境。如果身边确实没有Linux/Mac OS X环境，那么也可选择Windows。之所以不推荐Windows，原因有以下几点：

- Ruby/Rails在Windows上比较慢
- 一些gems和libraries在Windows环境不工作
- 社区大多使用Mac/Linux,如果在Windows环境使用出现问题可能难以解决

所以尽量选择Linux/Mac。强烈建议新手选择Ubuntu，网上这方面的教程较多，碰到问题也容易解决。没有还没有Linux环境，并且对Linux系统不熟悉，那么建议先在虚拟机下安装Linux。虚拟机的选择有：

- Virgrant
- VirtualBox
- VMware

以下教程主要针对Linux/Mac用户，如果实在要选择Windows，那么请在[此处](https://www.ruby-lang.org/zh_cn/downloads/)下载Windows下的二进制安装包RubyInstaller。


## 1. 安装RVM

RVM(Ruby Version Manager)是一个使安装、管理和多个Ruby环境切换变得简单的命令行工具。通过它安装不同版本的Ruby环境和gems包变得简单容易。更为详细的解释，请参考[RVM官网](https://rvm.io/)。

```
$ \curl -sSL https://get.rvm.io | bash -s stable
```

也可一步到位，直接安装RVM的同时安装上Ruby:

```
$ \curl -sSL https://get.rvm.io | bash -s stable --ruby=2.1.2
```

其中，`2.1.2`为指定的Ruby版本，当然也可省略版本号。安装完成后，重新加载RVM环境，使其配置有效。

```
$ source ~/.rvm/scripts/rvm
```

接下来检查下RVM是否安装成功：

```
$ rvm -v
```

如果显示`rvm xxx(stable) by Wayne E. ....`等信息便说明安装成功。

## 2. RVM安装Ruby环境

```
$ rvm install 2.1.2
```

安装过程可能比较漫长，耐心等待即可，编译安装完成后，Ruby和Ruby Gems也就安装成功。

## 3. 设置Ruby版本

```
$ rvm use 2.1.2 --default
```

这里, `2.1.2`为前面安装过的Ruby版本。

这时，可以检查是否正确安装配置：

```
$ ruby -v
```

```
$ gem -v
```

如果要安装`Rails`，直接通过：

```
gem install rails
```
便可完成安装。更多有关`gem`的命令，请通过:`gem --help`查询。
