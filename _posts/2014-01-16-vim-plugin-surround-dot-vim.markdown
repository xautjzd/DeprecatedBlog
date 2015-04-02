---
layout: post
title: "vim插件之surround.vim"
date: 2014-01-16 10:17
comments: true
categories: [Linux, Vim]
---
### Surround.vim插件简介

[Surround.vim] [1] 是一款关于括号、引号和xml标签匹配的插件，可以成对的添加、修改和删除。当然也可以自定义匹配项。下面就常用的功能分别对标记的添加、修改和删除一一介绍。

#### 添加

如现有一文本`Hello,wolrd`。光标处在文本中，然后输入ysiw",文本变成：

```
"Hello,world"
```

`yss`则将光标所在的当前行全部添加标签。如`yss)`则将当前行用()包围。

<!-- more -->

b, B, r和a分别是), }, ]和>的别名，t 则代表html/xml标签。

`ysst`,然后再输入html/xml标签，即可成对添加。如

```
Hello,world
```

输入`ysst<p>`后，变为：

```
<p>Hello,World</p>
```

类似的，`yssb`、`yssB`、`yssr`和`yssa`则给当前行添加相应的标记。

`<Ctrl-v>ySb`则给选定的文本添加()。

#### 修改

`cs`为修改的命令。如：`cs)}`将()换为{}，`csbr`将()换为[]。

#### 删除

`ds`为删除的命令。如：`dsb`删除(),`dsB`删除{},`dst`则删除相应的html/xml标签。

### 安装

先安装上[vundle] [2]或者[pathogen] [3]插件，然后再通过他们安装插件比较方便。下面以vundle举例：

在[~/.vimrc] [4]中添加：

Bundle 'tpope/vim-surround'

然后执行`BundleInstall`安装。

更多关于surround的细节，请通过`：help surround`查看。

### 其他

其实surround只是对vim中[text-object motion][5]的扩展，vim常见的text-object编辑功能有：

```
ci(, ci[, ci{：删除(),[],{}之间的所有字符并进入insert模式。类似的还有ci",ci'。
cit: 删除html/xml标签内所有的文本并进入insert模式。
di: 剪切配对符号间的文本，eg:di(, di{, ...
yi: 复制配对符号间的文本, eg:yi(, yi{, ...

ca, da, ya与ci, di, yi类似，只是包括比配符号本身。
```

[1]: https://github.com/tpope/vim-surround
[2]: https://github.com/gmarik/vundle
[3]: https://github.com/tpope/vim-pathogen
[4]: https://github.com/xautjzd/dotvim
[5]: http://vimdoc.sourceforge.net/htmldoc/motion.html
