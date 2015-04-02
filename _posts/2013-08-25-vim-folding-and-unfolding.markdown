---
layout: post
title: "vim文件的折叠与展开方式"
date: 2013-08-25 16:00
comments: true
categories: [Vim,Linux]
---
最近一直在用Vim学习Ruby,但是一直有个问题困扰：

那就是文件无法折叠，但是我记得以前看过Vim的视频，里面见别人用到了折叠与展开。文件比较小时，此功能便无用，但一旦文件量大时，折叠与展开便显得尤为重要了。

折叠的方式有以下几种：

1. manual
2. indent
3. syntax
4. marker
5. expr
6. diff

###1. Manual method

vim默认的折叠方式是此种方式，不需要设置即可。要启用其他方式还得采用`:set foldmethod=xxx`或者`:set fdm=xxx`来设置。

**使用方法**：

`v`或者`V`进入visual mode,然后选中要折叠的文字，按`zf`便可折叠，折叠后按`za`或者`zO`便展开。

同时也可以通过`zfnj`的方式将接下来的n行折叠。类似也有`zfnk`等;`zR`则打开所有的折叠。总结下来就是：

- zf		=> create a fold
- za		=> unfold
- zf#j 	=> fold down # lines
- zf#k  => fold up #lines
- zR		=> unfold all

###2. Indent method

缩进方式主要是根据代码缩进的方式来折叠/展开代码。要使用缩进方式，则需要做配置，`:set foldmethod=indent`或者在~/.vimrc中配置：`set foldmethod=indent`。

其快捷键如下：
zM		=> fold all
zR		=> unfold all
za		=> fold/unfold

###3. Syntax method

采用syntax方式，则只需如下配置即可：

	:set fdm=syntax

按键方式与上述相似
	
###4. Marker method
 
 使用markder方式，则做如下配置：

	:set foldmethod=marker
 或
 	
	:set fdm=marker
 
默认的marker折叠/展开标记为`{{{`和`}}}`. 

将要折叠/展开的代码通过`{{{ }}}`包含起来即可。当然也可以自定义标记。定义方法如下：

	:set foldmarker= start,end
	eg: set foldmarker= /*,*/

	/*
		 1. Ruby
		 2. Python
		 3. C++
		 4. PHP
	*/
	
快捷键如下：

- za		=> fold/unfold
- zM		=> fold all
- zR		=> unfold all

