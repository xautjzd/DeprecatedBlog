---
layout: post
title: "创建我的第一个rails程序"
date: 2013-07-30 17:22
comments: true
categories: Rails
---

##开启Mysql服务

我的一个rails程序是采用mysql数据库，不是默认的sqlite3.所以前提是已经安装了mysql。由于Mysql安装了好久，但是很少使用。所以服务没有启动，近来可能会频繁使用，便设置为开机自动启动了。设置方法为:`#systemctl enable mysqld.service`或者`service mysqld start`。

##安装mysql驱动

rails应用中使用msyql,需要Mysql对应的ruby驱动：msyql2。安装方式：
	
	$gem install mysql2

安装完成后可通过`$rails console`进行测试。测试方法为：

	>require 'mysql2'
	>client=Mysql2::Client.new(:host => "localhost", :username=>"root", :password=>"your_password", :database=>"your_db")
	=> #<Mysql2::Client:0xa058aac>
	> client.query("select version()")
	=> #<Mysql2::Result:0xa05233c>

这样表示已经连接成功。

到此为止，前期工作已经完成，后面就开始动手了。

<!-- more -->

##创建rails应用

	$rails new railsapp -d msyql  #指定数据库为mysql,否则采用默认的sqlite3
	$cd railsapp
	$rails server     #启动内置服务器

启动后，可以通过`http://localhost:3000`访问刚才创建的应用。一个简单的应用便就此完成了。

##添加应用

在上面建立的应用程序中，可以找到config/database.yml文件，里面是数据库的配置，默认会生成三个数据库development/test/production,同时也需要在其中添加username和password,分别对应自己的设置，database设为自己想要的数据库名。host设为localhost,port使用系统默认即可。

配置完成后，开始进行数据库的生成。
	
	$rake db:create

生成的只是空数据库，没有任何表。下面创建第一张表，通过rails的scaffold模式来生成表。

	$rails generate scaffold user username:xautjzd email:xautjzd@gmail.com 

通过此命令会创建相应的controller,views,model和数据库脚本，此时还没有创建表。通过：

	$rake db:migrate

执行上一步生成的数据库脚本。

##数据库回滚

通过：
	$rake db:rollback
回退上步操作，然后修改date\_create\_users\_rb.其中的up方法来建表，而down方法来删表。修改完后通过

	$rake db:migrate

再次生成新的数据库
