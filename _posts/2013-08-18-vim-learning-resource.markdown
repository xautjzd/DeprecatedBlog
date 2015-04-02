---
layout: post
title: "Vim学习资源"
date: 2013-08-18 13:48
comments: true
categories: [Vim,Linux]
---

### 实用的快捷方式

- gf  快速跳转到定义
- `<C + 6>`  返回到上次编辑的文档
- %  括号匹配{}[]()
- `#/*,g#/g*`  向前/向后搜索光标所在的词
- gi  跳转到上次编辑的位置
- gi  显示光标所在字符的编码
- gH  开始选择行模式
- vi"  选中"之间的文本(不包括")
- vi{  选中{之间的文本（不包括{）
- ci(  改变之间的文本
- di[  删除[之间的文本(不包括[)
- da[  删除[之间的文本(包括[),ca、va类似
- C  修改至行尾
- D  删除至行尾

<!-- more -->

- [{  跳转到光标所在位置的{.]},[(类似
- F/f+char  向左/向右跳转到char的位置
- `>>`  缩进光标所在行。eg:5>>
- `<<`  取消缩进光标所在行
- `>%`  大括号及括号内的内容都缩进(光标需放在{或者}上)
- ==  文本对其当前行
- =%  (re)indent the current braces{...}
- gg=G  全文对齐
- H  跳转到屏幕上方
- M  跳转到屏幕中间
- L  转到屏幕下方


### 参考文档

- [c9s](http://c9s.blogspot.com)的[Vim Hacks](http://c9s.blogspot.com/2009/08/vim-hacks-coscup.html)
- [Vim Tips](http://vim.wikia.com/wiki/Best_Vim_Tips)
- [Vim官网](http://www.vim.org/)

