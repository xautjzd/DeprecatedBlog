---
layout: post
title: "搭建Git服务器"
date: 2013-09-17 10:54
comments: true
categories: [Linux,Git]
---

从开始用Git到现在也已经有一年时间了，但一直都在本地开发，用于管理本地的代码，没有进行多人协作开发，所以也没有必要搭建一个Git服务器。

但就在昨晚，我在教研室给大家介绍Git工具时，感觉大家对这个工具貌似没有太大的热情，猜其原因，可能是因为大家对这个工具过于陌生，而我又讲的太过细节，所以他们可能听得有点烦。但是只有试过之后才能感觉其方便之处，我也希望教研室的同学都能掌握它，所以便决定在教研室搭建一个Git服务器，供大家使用，也思索着今后的项目都用git来进行管理。毕竟现在教研室只有我一人使用git,其他同学都用svn,甚至不用(其实用svn的同学不超过3个)，开发项目也难以统一，而我个人在使用过git后又不想转向svn，同时也非常希望身边的同学也能去使用git这么一个优秀工具，所以只能忽悠他们转向git了。不过经昨晚一役，证明了我忽悠人的本领完全不到家，看来今后得好好练练了。前奏有点过于冗长，下面进入正题吧。

<!-- more -->

由于此次git服务器是搭建在Linux平台，所以首先得有一台安装过Linux的pc,不过幸好我有一台台式机安装了Fedora,这样第一个要素就搞定了。接下来我选择的是ssh来作为git url的协议，因为ssh协议安全方便。所以服务器上还得安装ssh。比较好用的当属openssh了，我此前一直在fedora上用git管理我个人的代码，并且托管在GitHub上，所以这个环节也省了。没有安装的可以试试openssh，具体安装步骤问Google。

当然为了每次对远程库进行操作而不用输入用户名和密码，就需要将本地的公钥拷贝到服务器上对应的文件里，具体步骤如下：

###服务器

首先为了操作方便安全，需要在服务器上创建一个名为git的用户：

	#useradd git

接着进入到/home/git目录下新建一个.ssh目录,并且需要将.ssh目录group和others的写权限去掉，改为700|744|755皆可,否则ssh远程连接服务器还需要输入密码：

	git$ mkdir ~/.ssh
	git$ chmod 744 .ssh

服务端工作暂时完成

###客户端

进入~/.ssh/目录，生成公钥和密钥：

	$ ssh-keygen

然后一直回车，完成后会发现在~/.ssh目录下多了id_rsa和id_rsa.pub文件，然后将客户端生成的id_rsa.pub公钥拷贝到服务器上：

	$scp id_rsa.pub git@your_server_ip/~/.ssh/

以上操作在~/.ssh目录下进行，git为刚才服务器创建的用户(当然用户名可为其他用户名，只要和服务器对应便可)。此操作完成便会发现服务器上的~/.ssh/目录下多了一个id_rsa.pub文件。

现在转到服务器，将服务器上的~/.ssh目录下的id_rsa.pub文件改为authorized_keys。再重启sshd服务，使配置生效即可。

既然提到服务的开启与关闭，顺带将其操作列出来：

	#systemctl start sshd.service     #启动服务
	#systemctl stop sshd.service      #关闭服务
	#systemctl enable sshd.servie     #使服务开机便自动运行
	#systemctl is-enabled sshd.servie #查看服务是否开机启动
	#systemctl disable sshd.service   #取消开机自动运行
	#systemctl status sshd.service    #查看服务运行状态
	#systemctl restart sshd.service   #重启服务
	#systemctl reload sshd.service    #重新加载服务配置文件
	#systemctl --failed               #显示启动失败的服务

##SSH无密钥验证原理

客户端用ssh发起一个ssh连接时，服务端生成一个随机数并用客户端的公钥(保存在authorized_keys中)进行加密，然后发给客户端，客户端用私钥进行解密，并将解密后的数发送给服务端，服务端确认无误后便允许客户端进行连接了。

以上过程的前提是客户端已将公钥保存在服务端的authorized_keys文件中。

##搭建Git服务器

新建一个文件夹，用来作为Git服务器Repository,然后初始化。如我远程repository文件夹为/home/git/demo/,操作如下：

	$mkdir demo    #in /home/git/ directory
	$cd ~/demo/
	$git init

然后在客户端添加此远程库，便可进行代码的push和pull了。

	$git remote add origin git@your_server_ip:~/demo
	#after git add & git commit,run git push
	$ git push origin master

这样就把要管理的代码提交到Git服务器，并用Git来进行管理了。

至此，工作基本完成，后续还有好多东西需要研究，如代码的审查机制等，当然这个功能目前还用不到，但是想了解一下审查机制如何建立，后续再学习吧。
