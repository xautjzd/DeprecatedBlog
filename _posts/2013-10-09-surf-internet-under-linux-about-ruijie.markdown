---
layout: post
title: "Linux下锐捷客户端上网"
date: 2013-10-09 17:17
comments: true
categories: Linux
---
自己虽然一直用的校园网，但是由于教研室这块位置比较特殊，不需要使用锐捷客户端认证，但其他地方一般都需要。所以今早有个朋友在笔记本上安装了Ubuntu，但是无法通过锐捷web方式认证，下载的锐捷Linux版客户端安装后也无法上网，所以这方面我也不熟悉，只能求助Google了。由于众多高校的网络都是使用锐捷的这一套，所以大同小异，这方面的资料也不少，Google搜索很快便找到了解决方法，用华科的一个客户端即可，下载地址：[http://code.google.com/p/mentohust/](http://code.google.com/p/mentohust/)

下载后，切换到下载的目录，然后运行`sudo dpkg -i 'your deb packagename'`即可，安装过程中，一步一步按照其步骤输入相应信息即可。安装完成后，会将配置的信息存储在`/etc/mentohust.conf`文件中，也可进行修改。在安装的过程中，如果采用DHCP方式，在选择时应该注意，选择1或者2，千万别选择3，否则上不了网。各选项的含义是：

-d DHCP方式：0（不使用） 1（二次认证）2（认证后）3（认证前）

关于mentohust的详细参数解释，请参考[官网wiki](http://code.google.com/p/mentohust/wiki/Parameter)
