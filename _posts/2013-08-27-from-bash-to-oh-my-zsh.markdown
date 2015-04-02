---
layout: post
title: "Bash到oh-my-zsh的转变"
date: 2013-08-27 18:14
comments: true
categories: [Vim,Linux]
---
从开始使用到现在一直使用的bash,虽然以前听过ksh,csh,sh等，但都不曾用过，今年开始zsh便不断地出入在眼前，但没真正见人用过，也不知道效果咋样，所以也没做尝试。

另一个原因是各大linux默认都是bash,说明其功能不错，而且也处于懒的原因，就没折腾。但最近在使用tmux的过程中发现bash的提示符只显示`-bash4.2$`字样，并没有显示成`user@hostname directory`，在加上西安rubyist的熟人皓哥强烈推荐，这就坚定了我舍弃bash转到zsh的决心，二话不说，立马上GitHub上找到oh-my-zsh。就照着readme开始尝试，结果出现了错误，Google找到答案，是zsh没有安装才导致，所以就`yum install zsh`安装了zsh,随后在通过

`curl -L https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh | sh`

安装了oh-my-zsh。不过此时系统默认还是bash,所以还得更改系统默认的shell，方法如下：

###1. 修改/etc/shells文件

先通过`$which zsh`查看zsh的位置，我zsh位于/usr/bin/zsh。然后再查看/etc/shells中是否含有zsh:

`$< /etc/shells grep zsh`

如果结果中没有/usr/bin/zsh，则需要手动将/usr/bin/zsh添加到/etc/shells文件中。

###2. 更改默认的shell

通过`$chsh -s /usr/bin/zsh`更改系统默认shell，退出系统，重新登陆便会发现系统默认的shell已经变为zsh，同时也可以更改zsh默认的主题，在~/.zshrc中更改ZSH_THEME属性即可，其被选的值在[oh-my-zsh theme](https://github.com/robbyrussell/oh-my-zsh/wiki/themes)中任选一个即可。

经过以上两步，oh-my-zsh便安装完成。但是写博客时发现`rake new_post["xxx"]`时出现`zsh: no matches found: new_post`错误，Google找到答案，只需改为`rake 'new_post["xxx"]'`即可，原因是zsh会将一些特殊符号当作查找文件的通配符等，根源解决方法是：取消zsh的通配（Glob），即在~/.zshrc中加入`alias rake="noglob rake"`。

参考：[oh-my-zsh官网](https://github.com/robbyrussell/oh-my-zsh)
