---
layout: post
title: "Octopress目录结构"
date: 2013-07-18 14:27
comments: true
categories: [Octopress, Thinking] 
---
###Octopress博客目录结构

octopress博客的source目录结构大致如下:

    source/
    ├── _attachments
    ├── _includes
    │   ├── asides
    │   ├── custom
    │   │   └── asides
    │   └── post
    ├── _layouts
    ├── _nav_menu_items
    ├── _pages
    ├── _posts
    ├── blog
    │   └── archives
    ├── font
    ├── images
    │   ├── 2012
    │   │   ├── 01
    │   │   ├── 02
    │   ├── 2013
    │   │   └── 01
    │   ├── fancybox
    │   └── social
    ├── javascripts
    │   ├── asides
    │   └── libs
    ├── jsccp
    └── stylesheets
        ├── bootstrap
            └── syntax

当使用`rake generate`时，source的\_post目录中的markdown文件会被编译成html文件，并拷贝到public目录下，public目录结构与source目录结构一致，里面的内容为最终的静态页面。一般都是先`rake generate`生成静态页面，然后通过`rake preview`进行本地预览，如果显示正常，则`rake
deploy`部署到github上。如果特别熟练，也可以直接生成静态页面并部署，不需要本地预览。可以采用`rake gen_deploy`一步进行。
