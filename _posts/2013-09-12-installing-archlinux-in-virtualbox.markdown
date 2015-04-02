---
layout: post
title: "VirtualBox安装ArchLinux系统"
date: 2013-09-12 22:36
comments: true
categories: Linux
---

都说ArchLinux很适合折腾，趁今天有时间，就试着安装了一把，不过看ArchLinux的Beginners's Guide，照着其步骤来，结果还是看的云里雾里，看的人头大。便直接上Youtube上找了一个视频，顿时豁然开朗。安装概览如下：

##ArchLinux Install

1. 分区
2. 格式化分区
3. 挂载分区
4. 更改安装镜像
5. 安装基本系统
6. 生成fstab
7. Chroot到新系统
8. 配置系统
9. 开启网络服务
10. 创建初始化ramdisk环境
11. 设置root密码
12. 安装配置bootloader
13. 卸载分区并重启系统
14. 安装图形用户界面

详细步骤如下：

###1. 分区

虚拟机挂在iso镜像后，然后启动系统，进入后默认进入root提示符，然后输入：
	
	root#cfdisk

进行分区，一般分三个即可。最后分区结果如下：

	dev/sda1 / 8G
	dev/sda2 /swap 1G(在空间最后)
	dev/sda3 /home 4G

每个人的分区情况都可能不同，具体依照自己的分区来决定，以下操作都是根据我的分区来进行。

<!-- more -->

###2. 格式化分区

执行如下命令格式化分区

	#mkfs.ext4 /dev/sda1
	#mkfs.ext4 /dev/sda3
	#mkswap /dev/sda2
	#swapon /dev/sda2  #enable swap partion

###3. 挂载分区

	#mount /dev/sda1 /mnt #mount root partion
	#mkdir /mnt/home
	#mount /dev/sda3 /mnt/home  #mount home partion

###4. 更改安装镜像

镜像列表优先级从上往下，所以为了软件更新的速度，最好将国内的mirror放到最上面。我添加的源及方法如下：

	#vi /etc/pacman.d/mirrorlist
	
	Server = http://mirrors.163.com/archlinux/$repo/os/$arch
	Server = http://mirrors.ustc.edu.cn/archlinux/$repo/os/$arch
	Server = http://mirrors.sohu.com/archlinux/$repo/os/$arch
	Server = http://mirror.lzu.edu.cn/archlinux/$repo/os/$arch
	Server = http://ftp.tku.edu.tw/Linux/ArchLinux/$repo/os/$arch
	...

###5. 安装基本系统

通过pacstrap脚本安装基本系统，方法如下：
	
	#pacstrap base base-devel

###6. 生成fstab

通过下面的命令来生成fstab：

	#genfstab /mnt >> /mnt/etc/fstab
	
###7. Chroot到新系统

通过以下命令chroot到新安装的系统:

	#arch-chroot /mnt

使用chroot后，系统的目录结构将以指定的位置作为"/"目录

###8. 配置系统

系统的配置主要有locale和时区的配置。

- Locale

配置方法如下：

	#vi /etc/locale.gen
	#locale-gen

- 配置时区

系统默认是utc时区，我们需要换到utc+8时区，方法如下：

	#ln s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
	
###9. 开启网络服务

先通过ping命令查看网络是否正常，如果不能上网，则需要配置，方法有两种：1.dhcp  2.static ip。我用的是dhcp，所以只需要开启dhcp服务,方法如下：

	#dhcpcd interface_name

其中interface_name可以通过ifconfig或者ip addr查询。默认在虚拟机中便可上网，所以无需配置。但是安装完成重启系统后便不能上网，原因是dhcp服务没启动。(这是我所碰到的情况)

###10. 创建初始化ramdisk环境

ramdisk是通过软件将一部分内存(RAM)来模拟一个硬盘，提高访问速度。当然这只是针对内存过剩的情况下才使用，一般完全没有必要。如果您觉得内存完全用不完，为了有效的利用，可以创建ramdisk，毕竟RAM的访问速度非常快，差不多是固态硬盘的30倍。创建ramdisk的方法如下：

		#mkinitcpio -p linux

通过`#vi /etc/mkinitcpio.conf`来查看相应的配置信息。

###11. 设置root密码

设置密码的命令都通用:
	
	#passwd

然后输入符合要求的密码即可。当然平时操作尽量不要用root,所以为此可以新建一个用户。

###12. 安装配置bootloader

根据主板BIOS类型不同，安装和配置bootloader的方式也不同。
大致有两种类型：

1. 传统的BIOS
	- Syslinux
	- Grub
2. UEFI BIOS
	- EFISTUB
	- Gummiboot
	- Grub

我的主板是传统BIOS类型，采用Grub bootloader。二者的差别见图：

![](http://pic.yupoo.com/xautjzd/D9TU14LM/medish.jpg)

与传统BIOS相比，UEFI BIOS少了BIOS自检功能，这样节省了大量时间，从而加快平台的启动。

安装方法如下：

	#pacman -S grub-bios  #install grub bootloader
	#grub-install /dev/sda
	#grub-mkconfig -o /boot/grub/grub.cfg

其中grub-install将grub images拷贝到/boot/grub。
grub-mkconfig生成grub的配置，通过-o参数将配置输出到指定的配置文件，默认输出到标准输出。

###13. 卸载分区并重启系统

卸载分区前先通过`#exit`退出刚才新安装的系统，然后通过以下方法卸载分区:

	#umount /mnt/home
	#umount /mnt

然后通过`#reboot`重启系统。

###14. 安装图形用户界面

先确定能否联网：#ping www.google.com,如不能，则查看dhcp服务是否已经开启，可通过`dhcpcd interface_name`开启。在确保能上网的前提下通过：

	#pacman -S gnome xorg

安装gnome图形用户界面。

经过以上步骤，基本的安装便可完成。我也是安装了好几遍之后才对其安装过程有了大致的了解，写此篇博客的目的主要是为了记录自己的安装过程供今后参考、锻炼自己的写作水平和分享给那些安装ArchLinux过程中碰到问题的朋友参考。

###参考资料

1. [ArchLinux新手指南](https://wiki.archlinux.org/index.php/Beginners%27_Guide)

2. Youtube ArchLinux安装视频
