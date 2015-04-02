---
layout: post
title: "Octopress修改导航栏(Navigator)"
date: 2013-07-18 13:46
comments: true
categories: [Octopress, Thinking]
---
搭建好的Octopress导航栏默认只有Blog和Archives，远远不能满足要求，于是便想着在导航栏上添加几个菜单。方法如下：

    $rake new_page[About]
默认会在source目录中生成about/index.markdown文件，不过感觉这样影响视觉，便想着将生成的页面和其他页面放在一起，便可进行如下操作：

    $rake new_page[/blog/About]
这样便在source/blog目录中生成页面，方面管理。生成的页面目前还不能显示，还需编辑source/\_includes/custom/navigation.html文件：

    $vim source/_includes/custom/navigation.html

在其中加入
    <li><a href="{{ root_url }}/blog/about">关于我</a></li>

编辑完成后进行rake generate生成静态的html文件，然后rake preview便可以通过localhost:4000在本地预览。
