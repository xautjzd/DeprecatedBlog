---
layout: post
title: "终端分屏工具tmux的安装与常用操作"
date: 2013-08-08 16:12
comments: true
categories: Linux
---

##1. tmux简介

tmux是terminal multiplexer的简称，是一款终端分屏的工具，可以在同一屏幕中划分出多个独立的shell环境，这样便于对比，唯一的缺陷是窗口比较小而已。一个server可以有多个session,一个session可以有多个windows,一个windows可以有多个pane.具体见[官网](http://tmux.sourceforge.net/)介绍。

##2. 安装

采用相应系统的包管理器即可安装。我装的是fedora,现以fedora为例：

	#yum install tmux

包不到1M大小，很快便安装完成。

<!-- more -->

##3. 操作

首先，运行tmux。

	$tmux

然后可以水平分屏和纵向分屏。其常用的快捷键如下：

- 水平分屏 :`<c + b> "`即按下ctrl + b后，再按双引号(shift + '键)

- 垂直分屏 :`<c + b> %`

- 新建窗口 :`<c + b> c`

- 重命名窗口:`<c + b> ,`

- 窗口切换 :`<c + b> number`，其中number为窗体的编号，从0开始。

- 切换到bash:`<c + b> d`

- 切换回tmux:`$tmux attach`

- 查看帮助文档：`<c + b> ?`

1.新建一个session

	tmux new-session -s sessionname(自己指定)

2.杀死一个session

	tmux kill-session -t sessionname

3.杀死所有session

	tmux kill-server

4.列出新建的session

	tmux ls(tmux list-sessions)

4.附加一个session

	tmux a -t sessionname

另外，tmux也非常适合结对编程，当两个人可以连接同一台电脑时，其中一个人在终端上的操作，另一个在终端能清楚的看到。操作方式如下：

A操作：$tmux new-session -s test

B操作：$tmux a(ttach) -t test

这样之后，A在终端上的一切操作B都能看到。

其他具体快捷方式，请参考帮助文档。

也可以参考：

1.http://happycasts.net/episodes/41?autoplay=true

2.http://caok1231.com/blog/2013/04/14/tmux/

