---
layout: post
title: "Vim常用快捷键总结"
date: 2013-09-18 19:55
comments: true
categories: [Vim,Linux]
---

Vim的学习之路真的很长，永远有记不完的命令，永远会突然冒出一个新插件。不过我总算从Vim的荆棘中一路走过来了，现在真的是苦尽甘来，时刻体会它带给我的喜悦和惊奇。下面对我所学习所了解到的常用命令做一个基本总结：

###Normal mode:

`>>` indent current line

`n>>` indent the next n line

`.` repeat last command

`m,n>>` indent from m to n line


`==` autoindent current line

`n==` autoindent the next n line

`gg=G` autoindent the whole file

<!--more-->

`=i{` reindents 'inner block'(inside the braces)

`=a{` reindents "around block"(including the braces)

`=2a{` reindents 2 blocks(this block and containing block)


instead of "{", also can use "}" or "B".`=aB` equals `=a{`


`>i{` increase indent for inner block

`<i}` decrease indent for inner block

`>a{` increase indent for around block(including the brace)

`<a}` decrease indent for around block


With the cursor on `{` or `}`

`=%` autoindent the block(including matching brace)

`<%` or `>%` indents or unindents the block


###Insert mode:

`<c+t>` indent the current line

`<c+d>` reindent the current line

###Surroud plugin

以下是一些surround插件的功能：

	{
		xxx
		xxx
	}

normal模式下输入：dS{,结果变为:

	xxx
	xxx

	"hello world"

cS"'之后，结果变为：

	'hello world'

	<div>hello</div>

通过cSt然后输入`<p>`,结果变为：

	<p>hello</p>

当然也可以选进入visual模式，然后S"，便给选中的文本包含""。


以上命令主要是关于缩进和对齐的一个总结，关于surround插件做的总结也只是将所学列出，学过之后才感觉几乎毫无用处，所以不学也罢。其他的一些常用功能抽空再做总结。
