---
layout: post
title: "Fedora下使用sudo"
date: 2013-10-08 15:11
comments: true
categories: Linux
---
Linux下日常操作使用一般用户权限即可，但是往往有一些操作需要用到root权限，如服务的启动、软件的安装等，直接转到root下进行操作可不是一个好习惯，比较稳妥的方式就是使用sudo进行操作。首先检查系统是否已经安装`sudo`,接下来需要在`/etc/sudoers`文件下进行配置相应的权限。

在`root	ALL=(ALL)	ALL`这行下面添加`username	ALL=(ALL) NOPASSWD:ALL`即可。其中`username`为要使用sudo的用户，并且每次使用sudo时不需要输入root密码。

