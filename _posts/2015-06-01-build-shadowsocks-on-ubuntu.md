---
layout: post
title: "Ubuntu14.04上搭建ShadowSocks服务"
description: ""
category: Tech
tags: []
---

![](/images/20150601.jpg)

## 1. VPS选择

之前一直使用GoAgent作为破墙工具，不过后来有一阵用不成，即使更新到最新版，也未能如愿，后来忙于写论文，便用微软的[Bing](http://www.bing.com/)临时代替Google。用了一阵Bing,发现其实也挺好用，无论是UI还是搜索内容，都相当不错。只是偶尔想呼吸墙外空气，却未能如愿，始终给人不快的感觉。所以便有意选择付费服务。一直听说ShadowSocks搭建代理特别稳定，便开始留意VPS。可选的VPS很多，比较流行的当属Linode和Digital Ocean,不过Linode服务实在是太贵了，且最低配都感觉有点大材小用，没必要这么奢侈。便着重关注了下DO。可选的VPS有：

<!-- more -->

- [Linode](https://www.linode.com/)
- [Digital Ocean](https://www.digitalocean.com)
- [Bandwagon Host](https://bandwagonhost.com/)
- [RamNode](https://www.ramnode.com)

终于在昨天没忍住花5刀买了一个月的[Digital Ocean](https://www.digitalocean.com)服务。买了之后才知道通过已注册用户的邀请链接购买会有优惠，双方都能享受，所以如果有需要购买的用户，请通过熟人邀请注册，利人利己。[Bandwagon Host](https://bandwagonhost.com/)是买完后才发现的，最吸引人的是256M的内存4.99刀/年！简直太便宜了！买完DO便略后悔了。

Digital Ocean最低配5刀/月，内存512M，20G的SSD，这对跑个ShadowSocks绰绰有余，只是有点略贵。不过后来获得意外之喜，发现新注册用户可以获得10刀的优惠，不过官网可没有公布这样的讯息，无意之中网上浏览到的，找个promo code，然后在settings/billing中的promode code填入即可享受优惠，promo code的获取网址：http://digitalocean.youhuima.cc/ 。Google或者Bing搜[Digital Ocean promo code]，不少网站都有类似的优惠码。

Digital Ocean目前还不支持支付宝，但可通过PayPal付款，绑定国内的银联卡即可支付。注册并购买成功后登录进去，创建一个Droplet，服务器据说最好选择San Francisco的，其他地方的服务不是很好，不过没有亲测，未知其他地方地方的服务质量真实情况。


## 2. 搭建ShadowSocks服务

[ShadowSocks](https://github.com/shadowsocks/shadowsocks)源码托管在GitHub上，且有多个版本，有Python,GO，C#等等。不过通常都采用Python版。ShadowSocks代理的原理如下图所示：

![](/images/shadowsocks.png) 

ShadowSocks分为客户端与服务端，用户发送的Web请求，经由本地的ShadowSocks客户端发送给ShadowSocks远程服务端，远程服务端负责将请求发给用户请求的目标服务器，目标服务器将响应结果返回给SS服务端，经由SS客户端发送给用户。

安装过程可参考Shadow的[文档](https://github.com/shadowsocks/shadowsocks/wiki).我这里简要记录下。

### 2.1 安装ShadowSocks服务端

Debian/Ubuntu:
	
	#apt-get update
	#apt-get install python-pip
	#pip install shadowsocks

CentOS:
	
	#yum install python-setuptools && easy_install pip
	#pip install shadowsocks

### 2.2 开启ShadowSocks服务

	#ssserver -p 443  -k password -m aes-256-cfb

不过也可通过

	#ssserver -p 443 -k password -m aes-256-cfb --user nobody -d start

使其在后台运行

不过大多更倾向于将配置保存于配置文件中，创建一个配置文件/etc/shadowsocks.json,然后填入以下内容：

	{
    		"server":"my_server_ip",
    		"server_port":8388,
    		"local_address": "127.0.0.1",
   		"local_port":1080,
    		"password":"mypassword",
    		"timeout":300,
    		"method":"aes-256-cfb",
   		"fast_open": false
	}

只需更改server IP和password即可。可参考：[https://github.com/shadowsocks/shadowsocks/wiki/Configuration-via-Config-File](https://github.com/shadowsocks/shadowsocks/wiki/Configuration-via-Config-File)

以上配置适用于个人，但不便与人分享，毕竟密码属于私有的东西。若要与人共享SS服务，可创建多用户的配置，配置如下：

	{
    		"server": "my_server_ip",
    		"port_password": {
        		"8381": “password1",
        		"8382": "password2",
        		"8383": "password3",
        		"8384": "password4"
    		},
		"local_address": "127.0.0.1",
   		"local_port":1080,
    		"timeout": 300,
    		"method": "aes-256-cfb"
}

不同端口对应不同用户，并设置不同密码。

配置完成后，通过：

	#ssserver -c /etc/shadowsocks.json

在前台开启SS服务。或者也可通过：

	#ssserver -c /etc/shadowsocks.json -d start
	#ssserver -c /etc/shadowsocks.json -d stop

在后台开启服务。

多用户具体可参考：[https://github.com/shadowsocks/shadowsocks/wiki/Configure-Multiple-Users](https://github.com/shadowsocks/shadowsocks/wiki/Configure-Multiple-Users)

【可选操作】为了更快的服务，可开启TCP Fast Open，不过需要多耗费约30M的内存。以下为截取官方内容：

>After optimizing, a busy Shadowsocks server that handles thousands of connections, takes about 30MB memory and 10% CPU. Notice that at the same time, Linux kernel usually uses >100MB RAM to hold buffer and cache for those connections. By using the sysctl config above, you are trading off RAM for speed. If you want to use less RAM, reduce the size of rmem and wmem.

具体操作见[https://github.com/shadowsocks/shadowsocks/wiki/TCP-Fast-Open](https://github.com/shadowsocks/shadowsocks/wiki/TCP-Fast-Open)。


### 2.3 开启SS客户端

GUI客户端各平台都有。

Windows平台下载地址：[http://sourceforge.net/projects/shadowsocksgui/files/dist/](http://sourceforge.net/projects/shadowsocksgui/files/dist/)

Linux平台无须使用GUI客户端，只须如2.1步骤安装SS，然后通过：

	#sslocal -s server_ip -p port -k password

开始客户端监听。

Android客户端需要上Google Play下载，我这有现成的，如有需要，请联系我。

### 2.4 浏览器配置

Chrome浏览器，请使用[SwitchOmega](https://github.com/FelisCatus/SwitchyOmega)。然后在其中加入本地代理即可。协议选择sockv5，监听的端口为1080.





