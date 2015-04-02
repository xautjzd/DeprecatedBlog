---
layout: post
title: "Octopress配置Disqus插件"
date: 2013-07-18 15:37
comments: true
categories: [Octopress, Thinking]
---
###添加Disqus插件
看到不少人博客上都有Comments功能，便也想给自己的博客添加上。经过搜寻一番，发现大多用的都是Disqus，而且octopress其实内置了其功能，只是默认没有设置.编辑博客主目录下的config.yml文件即可：
    $vim _config.yml

找到：
    #Disqus comments
    disqus_short_name: 
    disqus_show_comment_count: false

填上自己注册的disqus账号的short name，并将false改成true即可。

**注：Disqus一定要和yourname.github.com关联**
