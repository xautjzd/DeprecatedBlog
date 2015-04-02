---
layout: post
title: "Linux下截图工具shutter的安装与配置"
date: 2013-08-16 16:57
comments: true
categories: Linux
---
我一直使用的是Fedora17，自带的截图工具实在不敢恭维，但也就这样断断续续的用着，不过也用的不多。但今天突然鬼使神差的搜了下其他的截图工具，Google搜了下，发现好多提到shutter，既然这么多文章都提到，说明肯定着实不赖，便尝试了下。安装及配置如下：

###1.安装
安装过程很简单，执行下面命令即可：
	#yum install shutter
###2.配置
QQ截图快捷键`<ctrl>+<alt>+A`用习惯了，所以也对shutter继续保留这个快捷键。具体配置方法如下：
在System Tools>System Settings>Keyboard>Shortcuts>Custom Shortcuts中添加了三个快捷键：

- 截图整个屏幕（shutter -f）

- 截图当前活动窗口(shutter -a)

- 截图选定区域(shutter -s)
	
具体配置及对应的快捷键设置参考下图：
![](/images/shutter-config.jpg)
