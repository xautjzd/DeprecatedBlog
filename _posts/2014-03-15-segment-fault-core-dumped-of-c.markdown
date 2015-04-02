---
layout: post
title: "C语言中的Segment fault问题"
date: 2014-03-15 20:47
comments: true
categories: [Linux, C] 
---
![](img /images/20140315.jpg)

## 什么是Segment fault?

>  a segmentation fault (often shortened to segfault) or access violation is a fault raised by hardware with memory protection, notifying an operating system (OS) about a memory access violation; on x86 computers this is a form of general protection fault.

以上为[Wikipedia](http://en.wikipedia.org/wiki/Segmentation_fault)对段错误的解释。用通俗易懂的话来说就是访问越界，访问了不存在或者受操作系统保护的内存，通常都是由于数组越界或者指针引起。

## 产生段错误的原因

1. dereferencing NULL
2. dereferencing an uninitialized pointer
3. deferencing a pointer that has been freed/out of scope
4. writing off the end of an array
5. recursive function that uses all of the stack space

<!-- more -->

## 什么是core文件？

在调试段错误前，不得不提到core文件。那么什么是core文件呢?core文件其实就是当程序崩溃时保存的该进程在内存中的映像(同时包含调试信息),主要用于调试。

## 如何调试？

像VS等IDE集成度太高，在方便快捷的同时也会将人培养成傻瓜，培养成码农。所以要想抱着以学习的心态来学习，最好转到Linux/Mac OS平台下，通过gcc/cmake等command-line式的编译器来进行代码的编译，当然我这里主要指的是c/c++。

Linux段错误时默认不会生成core file，core file的大小被设置为0,可通过`ulimit -a`查看。所以首先得通过`$ulimit -c unlimited`进行设置，以便能够生成core file。但在shell里设置的话，只是针对当前会话有效，如果想永久生效，需要将其写到配置文件中，如~/.bashrc, /etc/profile/, /etc/security/limits.conf等中。

设置完成后，便可通过gdb和gcc来调试程序了。如果一个程序存在段错误问题，那么执行`$gcc filename.c -g -o filename`进行编译后，在运行`filename`的时候，会在当前的目录下产生一个core文件。那么这个时候便可以利用core文件进行调试了。调试方法为:

    $gdb [exec file] [core file]

有关gdb的详细用法，请参考相关文档去吧。

段错误实质上是操作系统内核产生的一种中断信号，信号为12。有关信号的知识，请参考操作系统相关的书籍。可通过`kill -s SIGSEGV processid`来给指定的进程id发送段错误信号，段错误默认处理方法是终止程序的运行。
