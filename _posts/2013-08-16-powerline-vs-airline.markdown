---
layout: post
title: "安装Powerline过程中的收获"
date: 2013-08-16 22:12
comments: true
categories: Vim
---
Powerline插件已经多次耳闻目见，但是一直没做尝试，今天再次看到便忍不住试了下，结果还没成功。可能是由于字体的原因吧，在找答案的过程中邂逅了airline,据说比powerline加载更快，而且还无需安装字体。所以便果断地换为airline。只需在vimrc中加入`bundle bling/vim-airline`即可。当然前提是在~/.vimrc中已有如下配置：

```sh
set laststatus=2  "Always show the status line
set noshowmode
set t_Co=256

```
配置好后效果如下图所示：
![](/images/airline.jpg)

配置好后，在bash中显示没问题，但是在tmux中显示就有问题了，先前配置的效果无法显示。网上也找了好久答案，才得以解决，方法如下：

**1.$vim ~/.tmux.conf**
	
在~/.tmux.conf文件中添加如下代码：

	set -g default-terminal "screen-256color"

**2.$vim ~/.bashrc**

在~/.bashrc中添加如下代码：

	alias tmux="tmux -2"

`tmux -2`是强制tmux的终端支持256种颜色。

配置好后，显示没问题，但是在写博客的过程中发现vim突然不能输入中文了，不知为何。最后在~/.vimrc添加：
	set guifont=*
就顺利解决，不过原因待深究，要学的东西太多。
