---
layout: post
title: "Tmux常用操作总结"
date: 2013-12-04 19:32
comments: true
categories: Linux
---
以前也写过一篇关于[tmux的文章][1],大概对tmux从简介、安装到操作已有简单的介绍，但由于是刚使用tmux时所写，总感觉操作部分写的不是很好，不够全面，所以便出现了此篇，算是填补前一篇的不足吧。

前边的操作前缀是Ctrl+b组合键，这两个键相隔甚远，操作起来太别扭，后来便在`~/.tmux.conf`配置文件中更改成`Ctrl+a`前缀了。具体配置见GitHub上[我的tmux配置][2]。

### **Tmux常用操作**

####1. 新建Session

```
$tmux new -s sessionname
```

####2. 杀死指定Session

<!-- more -->

```
$tmux kill-session sessionname
```

####3. 杀死所有Session

```
$tmux kill-server
```

####4. 列出创建的Sessions

```
$tmux ls
```

####5. 附加指定Session

```
$tmux a -t sessionname
```

####6. 离开Tmux到shell环境

```
$<prefix> + d
```

**注**：其中prefix即为前边所提到配置好的Ctrl+a(tmux默认为ctrl+b),`<prefix> + d` 即为Ctrl+a+d三个键的组合。后面如无特别说明，也指这样的键组合。`离开tmux环境`指的是首先在shell下tmux new -s sessionname进入到tmux环境，然后`<prefix> + d` 切换到shell环境，在shell下又可以通过`tmux a -t sessionname`切换到tmux环境。

以下的操作都在tmux环境里面进行：

####7. 新建Window

```
$<prefix> + c
```

####8. 水平分屏

```
$<prefix> + -
```
默认为",需要在~/.tmux.conf中配置

####9. 垂直分屏

```
$<prefix> + |
```

####10. 窗口重命名

```
$<prefix> + , # 默认为%
```

####11. 窗口切换

```
$<prefix> + n  # n为窗口的编号，从0开始，编号可以在屏幕最下方看到
```

####12. 同一窗口中pane之间的切换

```
$<prefix> + 方向键
```

####13. 关闭当前窗口中的所有panes

```	
$<prefix> + !
```

####14. 显示时间

```
$<prefix> + t
```

####15. 关闭当前窗口

```
$<prefix> + : 
```	
然后输入`kill-window`即可关闭。

####16. 查看帮助文档

```
$<prefix> + ?
```

[1]: http://xautjzd.github.io/blog/2013/08/08/tmux-use-and-configuration/
[2]: https://github.com/xautjzd/dotvim

