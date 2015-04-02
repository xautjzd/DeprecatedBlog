---
layout: post
title: "Unix C的文件指针与文件描述符"
date: 2014-05-21 09:59
comments: true
categories: C 
---

![](/images/20140521.jpg)

AISC C中通常用文件指针FILE *进行文件的操作，如fopen, fclose, fread, fwrite, fscanf, fprintf等函数，都是通过文件指针进行文件的一系列操作；而类Unix系统则大多用文件描述符(file descriptor)进行文件的操作，如open, close, read, write等函数，文件描述符是一个整数，是文件描述符表(file descriptor table)中的索引(文件描述符表其实是维护进程打开的文件)。当进程打开或者创建一个文件，内核便会在此进程对应的文件描述符表中分配一个位置，然后便可通过文件描述符操作文件。

<!-- more -->

在内核中，每个进程都拥有自己的文件描述符表，表示此进程已打开的所有文件。文件描述符表中每一项其实是一个指针，指向文件表(file table)中用于描述打开文件的数据块——file对象，file对象其实是一个file结构体，有关file结构体的定义，请参考:include/linux.fs.h文件。file结构体包含了文件的打开模式、读写位置等重要信息，当进程打开一个文件时，内核便会创建一个新的file对象。这里要注意的是,file对象不专属于某个进程，不同进程的文件描述符表中的指针可以指向相同的file对象，从而达到共享打开的文件。file对象有引用计数，记录引用这个对象的文件描述符个数，只有当引用计数为0，内核才会销毁该file对象，所以某个进程关闭文件，并不影响与之共享同一个file对象的进程。file对象中包含一个指针，指向dentry对象。dentry对象代表一个独立的文件路径，如果一个文件被打开多次，那么便会建立多个file对象，但他们都指向同一个dentry对象。

dentry对象又包含一个指向inode对象的指针。inode对象代表一个独立的文件，因为存在硬链接与符号链接，因此不同的dentry对象可以指向同一个inode对象，inode对象包含最终对文件进此操作所需的所有信息，如文件系统类型、文件操作方法、文件权限、访问日期等。

打开文件后，返回的文件描述符实质上是文件描述符表的索引，根据索引对应的指针访问对应的file对象，然后根据file对象访问对应的dentry，根据dentry对应的inode，从而实现文件的操作。

## 转换关系

有关文件指针与文件描述符及文件路径(包含文件名)之间的转换关系如下：

- 文件路径->文件指针: filepath--fopen()-->FILE *;
- 文件路径->文件描述符: filepath--open()-->fd;

- 文件描述符->文件指针: fd--fdopen()-->FILE *;
- 文件描述符->文件路径: fd--readlink(/proc/%getpid()/fd/%fd)-->filepath;

- 文件指针->文件描述符: FILE *--fileno()->fd;

下面通过一个例子展示文件描述符与文件指针间的关系:

```c
#include <stdio.h>
#include <unistd.h>

int main(char **argv, int argc)
{
	int fd;
	FILE *fp;
	char proclnk[255];
	char filepath[255];

    # test.txt为已存在的文件
	fp = fopen("test.txt", "r");
	if (fp != NULL) {
		fd = fileno(fp);
		sprintf(proclnk, "/proc/self/fd/%d", fd);
		readlink(proclnk, filepath, 255);
		
		printf("fp->fd->filepath: %p->%d->%s\n", fp, fd, filepath);
	}

	return 0;
}
```
