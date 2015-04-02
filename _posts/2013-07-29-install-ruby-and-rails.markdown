---
layout: post
title: "Fedora17下搭建Ruby和Rails环境"
date: 2013-07-29 20:59
comments: true
categories: Ruby
---

不同的项目所用的ruby版本不同，所以为了方便不同项目ruby版本的切换，需要在同一个系统中安装多个ruby版本，并且针对不同的项目在不同的版本间切换，为了方便ruby版本的管理，采用[RVM](https://rvm.io/)进行管理。

##1.安装RVM

	#curl -L https://get.rvm.io | bash -s stable

一会儿之后rvm便安装完成,安装位置为/usr/local/rvm目录下，网上很多教程都是使用一般用户权限管理，但是我也尝试过采用一般用户权限安装，但是始终不会安装在~/usrname/.rvm目录下，还是提示安装在/usr/local/rvm下，但是没有写的权限。可能是fedora系统的原因吧，没有深究。使用：

	#source /usr/local/rvm/scripts/rvm

使rvm配置生效。然后采用：

	#rvm -v

查看rvm的版本。同时也可以通过`rvm info`查看rvm相关信息。

<!-- more -->

##2.安装Ruby环境

使用`rvm install 1.9.3`会默认选择`http://ruby-lang.org`网站下载ruby源码然后进行编译，这样太慢。幸好淘宝提供了[ruby的下载源](http://ruby.taobao.org/mirrors/ruby/)，我此次便采用的是先在淘宝的ruby源下载我想要的ruby版本1.9.3-p448，下载完成后，将其放到/usr/local/rvm/archives/目录下，然后再执行`rvm install 1.9.3-p448`，它便能识别已有的ruby源码包，进行解压和编译一系列过程。大致几分钟便可完成。

下面是我采用一般用户权限安装ruby出错。
	
```ruby
	$ rvm install 1.9.3-p448
	Searching for binary rubies, this might take some time.
	No binary rubies available for: fedora/17/i386/ruby-1.9.3-p448.
	Continuing with compilation. Please read 'rvm help mount' to get more information on binary rubies.
	Installing requirements for fedora, might require sudo password.
	Requirements installation successful.
	Installing Ruby from source to: /usr/local/rvm/rubies/ruby-1.9.3-p448, this may take a while depending on your cpu(s)...
	ruby-1.9.3-p448 - #downloading ruby-1.9.3-p448, this may take a while depending on your connection...
	Archive checksum did not match, downloading again.
	rm: cannot remove `ruby-1.9.3-p448.tar.bz2': Permission denied
	curl: Can't open 'ruby-1.9.3-p448.tar.bz2'!
	curl: try 'curl --help' or 'curl --manual' for more information
	There was an error(23), please check /usr/local/rvm/log//*.log. Next we'll try to fetch via http.
	Trying ftp:// URL instead.
	curl: Can't open 'ruby-1.9.3-p448.tar.bz2'!
	curl: try 'curl --help' or 'curl --manual' for more information
	There was an error(23), please check /usr/local/rvm/log//*.log
	There has been an error fetching the ruby interpreter. Halting the installation.
```

##3.设置Ruby版本

通常系统都会安装多个Ruby版本，可通过`rvm list`查看系统已安装的ruby版本。但需要指定某一版本为系统默认版本。

	#rvm use 1.9.3 --default

我使用的版本为1.9.3，所以指定为默认版本。

安装Ruby的过程中会自动安装gem，通过下列方法查看其版本

	#ruby -v
	#gem -v

同时替换gem的下载源为淘宝源：

	#gem source -r https://rubygems.org
	#gem source -a http://ruby.taobao.org

##4.安装Rails环境

采用：

	#gem install bundler rails

安装bundle和rails。

安装完成后进行测试：

	#rails -v
	#bundle -v
