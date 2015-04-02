---
layout: post
title: "Linux硬链接与软链接"
date: 2013-10-10 09:42
comments: true
categories: Linux
---
链接的概念其实不仅限在Linux中，在类Unix和Windows中也存在，只是网上资料大多都讨论的是类Unix的链接。下面主要对所了解的类Unix下的链接谈谈自己的认识。

###链接存在的目的

链接的出现主要是为了解决系统中文件的共享，同时有其他附加的好处：隐藏真实文件路径、增加权限安全及节省存储。简单的举例说明：

Linux中有7种run level(0-6),其中0代表关机，1代表单用户模式(用于系统维护，禁止远程登陆),2代表多用户状态(不支持NFS)，3代表完全的多用户模式，4系统保留(未使用),5代表X11模式(GUI模式)，6则代表重启。

这7种模式分别对应/etc/rc.d/rcN.d目录(N指0-6之间的数字)，存储的是每种启动模式下要启动的程序，但实际的程序其实存储在/etc/rc.d/init.d目录中，/etc/rc.d/rcN.d中都是链接而已，链接到/etc/rc.d/init.d目录中对应的程序(这样做的目的是为了管理上的方便，试想一下，如果有多个runlevel包含同一个程序，需要对这个程序的启动脚本进行修改时，只需更改/etc/rc.d/init.d中的实际文件，而不需要改动/etc/rc.d/rcN.d)。

###链接的分类

链接分为两种：硬链接(hard link)与阮链接(soft link)。谈链接就不得不谈inode，所以先简单地介绍下inode。

<!-- more -->

**inode**

类unix中，文件被分为两部分：用户数据(user data)和元数据(metadata)。用户数据，即文件数据块(data block),数据块是记录文件真实内容的地方，而元数据则是记录文件的附加属性，如文件大小、创建时间、所有者等信息。而inode则负责存储这些元数据，inode确切的说是一个数据结构，包含了文件的所有信息(文件名除外)。inode包含的详细信息为：

- Inode number
- Access Control List(ACL)
- Extended attribute
- Direct/indirect disk blocks
- Number of blocks
- File access, change and modification time
- File deletion time
- File generation number
- File size
- File type
- Group
- Number of links
- Owner
- Permissions
- Status flags

通过`ls -i`或者`stat filename`可查询文件对应的inode信息

文件新建时，内核会分配一个inode,每个文件的inode号唯一，可以简单地将其理解成指针，指向对应文件的具体的存储位置。访问文件时，inode会被复制到内存，然后根据inode将对应的文件复制到内存。

**硬链接**

![](http://pic.yupoo.com/xautjzd/DdZo1Za8/medish.jpg)

如图，硬链接其实就是在现有文件上添加了一个别名，他们有共同的inode,但硬链接有以下不足：

1. 不能跨文件系统(inode号仅在同一文件系统下唯一，当挂载多个文件系统后，便可能会出现inode号重复的现象，所以不能跨文件系统)
2. 只能针对文件创建硬链接，不能对目录创建

每个inode都有一个链接计数器,默认文件的inode计数器值为1,每当创建一个硬链接，计数器值便加1，而删除文件时，其实是计数器值减1，只有当计数器为0时，文件才从物理磁盘上删除。

下面看一个实例：

	265092 -rw-rw-r--   2 fedora fedora         0 Oct 10 14:16 test
	265092 -rw-rw-r--   2 fedora fedora         0 Oct 10 14:16 testdl
	265164 lrwxrwxrwx   1 fedora fedora         4 Oct 10 14:18 testsl -> test

其中test为新建的测试文件，testdl是在test上建立的硬链接，testsl是在test之上的软链接。可以发现test与testdl的inode号相同，而test与testsl的inode号则不同，在创建了硬链接之后，test与testdl的计数器变成2了。

**软链接**

软链接(也称符号链接 symbol link)刚好弥补了硬链接的不足，不存在文件系统的限制，同时也可以创建指向目录的符号链接。所以现在广泛使用的一般是软链接，它具有更强的灵活性。但它同时也具有硬链接没有的缺点，那就是：

1. 软链接包含原有文件的路径信息，一旦原文件移到其他路径下，再访问软链接，便找不到了，硬链接则无影响。 
2. 系统会为软链接分配额外的空间用于建立新的inode并保存原文件的路径

###软链接与硬链接的区别

1. 硬链接与原文件inode号相同，表明他们是同一个文件；而软链接与原文件inode号不同，说明他们是两个不同的文件。(上图便可看出)
2. 文件属性上软链接明确标明了是链接文件，而硬链接则没有，因为在本质上硬链接与原文件是完全平等的关系。
3. 链接计数器不同，软链接的计数器不会增加。
4. 文件大小不同，硬链接文件显示的大小与原文件相同，而软链接则显示的大小与原文件不同。

###参考文档

1. http://www.cnblogs.com/ovliverlin/archive/2008/10/28/1321521.html
2. http://www.ibm.com/developerworks/cn/linux/l-cn-hardandsymb-links/

