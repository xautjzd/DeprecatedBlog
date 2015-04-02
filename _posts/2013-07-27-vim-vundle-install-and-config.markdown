---
layout: post
title: "Vim下的的插件管理神器——Vundle"
date: 2013-07-27 20:38
comments: true
categories: [Linux, Vim]
---
断断续续用Vim也不少时间了，但是从来没有进行过复杂的Vim配置，每每需要插件都是网上寻求安装方式。但是当插件多了管理也便变得繁琐，最后终于让我结识了插件管理神器——Vundle，用过的人都说好用，所以我便也尝试了，网上也有一部分人采用pathogen来进行插件管理，但是据说没有Vundle好用，也便没有尝试，下面对我使用Vundle做一个总结。

首先Vundle采用git插件的git repo以及vim-scripts维护的GitHub repo, 自动安装, 更新和卸载插件. 把这些繁杂的工作变得简单, 甚至, 成为一种享受.

##安装
[Vundle地址](https://github.com/gmarik/vundle),上面安装及配置步骤已经很详细，我在此再赘述下：

1.拷贝Vundle
    $ git clone https://github.com/gmarik/vundle.git ~/.vim/bundle/vundle

上面步骤将vundle拷贝到本地的～/.vim/bundle/vundle目录下

2.Vundle配置

以下是我的配置文件：

<!-- more -->

```sh
    set runtimepath+=~/.vim_runtime

    source ~/.vim_runtime/vimrcs/basic.vim
    source ~/.vim_runtime/vimrcs/filetypes.vim
    source ~/.vim_runtime/vimrcs/plugins_config.vim
    source ~/.vim_runtime/vimrcs/extended.vim
    source ~/.vim_runtime/vimrcs/taglist.vim

    let Tlist_Ctags_Cmd='/usr/bin/ctags' 
    let Tlist_Inc_Winwidth=0
    let Tlist_Process_File_Always=1
    let Tlist_File_Fold_Auto_Close=1
    set autochdir

    colorscheme molokai

    try
        source ~/.vim_runtime/my_configs.vim
        catch
        endtry

        "Below is vundle configuration
        set nocompatible               "disable vi compatibility
        filetype off                   " required!

        set rtp+=~/.vim/bundle/vundle/  "set runtimepath
        call vundle#rc()

        " let Vundle manage Vundle  
        Bundle 'gmarik/vundle'

        "My Bundles here
        Bundle 'tpope/vim-fugitive'
        Bundle 'Lokaltog/vim-easymotion'
        Bundle 'rstacruz/sparkup', {'rtp': 'vim/'}
        Bundle 'tpope/vim-rails.git'

        "vim-scripts repos
        Bundle 'L9'
        Bundle 'FuzzyFinder'

        "snippets
        Bundle 'http://github.com/gmarik/snipmate.vim.git'

        "Syntax highlight
        Bundle 'cucumber.zip'
        Bundle 'Markdown'

        "Utility
        Bundle 'SuperTab'
        Bundle 'repeat.vim'
        Bundle 'surround.vim'
        Bundle 'file-line'
        Bundle 'scrooloose/nerdtree'

        "Navigation
        Bundle "http://github.com/gmarik/vim-visual-star-search.git"

        "non github repos
        Bundle 'git://git.wincent.com/command-t.git'
        "git repos on your local machine (ie. when working on your own plugin)
        "Bundle 'file:///Users/gmarik/path/to/plugin'

        filetype plugin indent on     " required!
```

其中将需要的插件用Bundle添加进来即可。如需要NERDTree插件，在github上找到它，找到的地址为：https://github.com/scrooloose/nerdtree.git

则在~/.vimrc里添加：
    Bundle 'scrooloose/nerdtree'

3.安装

推出刚才的配置文件，然后重新打开vim,并且执行:BundleInstall，这样NERDTree插件便安装完成，可以在~/.vim/bundle目录中查看。Vundle的特色在于使用git管理插件，更新方便，并且支持搜索。

:BundleInstall!更新插件，:BundleClean删除插件(只需在.vimrc中注释相应行), :BundleSearch查找插件。不同电脑间的同步只需通过.vimrc来实现（前提：安装git）。

安装插件就是这么简单！还没有体验的赶紧体验吧！
