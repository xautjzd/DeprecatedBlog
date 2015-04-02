---
layout: post
title: "Vim的代码自动补齐插件——UltiSnips"
date: 2013-08-03 15:12
comments: true
categories: [Linux, Vim]
---

暑假时间充足，便又开始学习自己喜欢的Ruby。而学Ruby的最佳环境是Mac,其次是Linux,最次是Windows。Mac买不起，只能在Linux上折腾了，一台台式机装的Fedora17，自己的本是xp系统，装了不少微软的一套东西，毕竟教研室的项目都是在.net环境下进行的，不敢轻易换系统，所以便在本上装了个VirtualBox虚拟机，虚拟了一个Ubuntu。上面也配好了Ruby环境，毕竟本方便，带到哪里都可以学，但平时的Linux编程都是在台式机下，毕竟性能比虚拟机好。

而学习Ruby一般都是在Vim/Emacs/SublimeText 2下，RubyMine貌似很适合开发Ruby，由于是商业产品，没钱购买也就舍弃了，毅然决然的选择了Vim.都说高手使用的是Vim，想必必有可取之处。但是Vim的学习路线比较陡峭，开始是一段痛苦期，经过一段时间的摧残后，甜蜜的时光便来临了，各种强大而高效的插件让你目瞪口呆，顿时感觉其他IDE都蒻爆了。幸好我以前对Vim的基本操作便有了了解，所以再次学习起来便不那么痛苦，甚至不想回到Windows环境，不想再用其他的Editor。我现在用的插件并且给我印象深刻的大致有这么一些：Vundle,Ctrlp/command-T,UltiSnips/Snipmate,YouCompleteMe/SuperTab,NerdTree,Tagbar,FuzzyFinder,vim-rails，Markdown等。

<!-- more -->
其中Vundle作为Vim的插件管理神器必不可少，让安装插件变得非常方便，类似的插件也有pathogen。具体安装方法见[GitHub](https://github.com/gmarik/vundle).也可以参考我写的一篇关于Vundle的[博文](http://xautjzd.github.io/blog/2013/07/27/vim-vundle-install-and-config/)。

而CtrlP则绝对是文件切换的神器，在多个文件间来回切换。也可以用:vs垂直分屏或者:sp水平分屏,这样最适合多个文件间的对比。<ctrl-p>调出CtrlP候选文件,然后通过Up/Down键来选择文件。

UltiSnips则是自动补齐代码片段的神级插件，功能类似的有Snipmate插件。UltiSnips对常见的各种语言都有支持。代码补齐是通过编辑的文件后缀名来区分，如编辑xxx.html时，输入ul然后按Tab键则自动生成了`<ul><ul>`片段，其他语言也类似，都有相应的关键字，具体每种语言的关键字参考UltiSnips目录下的xxx.snippets，自己也可以补充。

YouCompleteMe插件是一个代码提示功能，输入一部分然后就会出现候选的部分可供选择，不需要全部输入。类似的插件还有SuperTab。通过名字也可以看出它提供的候选词中也包括刚才输入的单词。默认的选择是通过Tab键来确定的，但由于和UltiSnips冲突，所以需要换默认的快捷方式，方法如下：

	"set YouCompleteMe trigger key 
	let g:ycm_key_list_select_completion = ['<c-n>', '<Down>']
	let g:ycm_key_list_previous_completion = ['<c-p>', '<Up>']

NerdTree提供一个目录结构，让习惯图形界面的朋友找到亲切感，作用不必多说。

Tagbar则配合ctags则提供文件的导航，将文件的关键字提取出来。ctags需要在目录下生成一个tags文件，生成方法:

	ctags -R yourdir  #生成tags文件

FuzzyFinder是一个模糊匹配的文件搜索插件。
