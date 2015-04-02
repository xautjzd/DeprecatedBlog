---
layout: post
title: "更换Octopress主题"
date: 2013-08-17 22:56
comments: true
categories: [Octopress,Thinking]
---
Octopress博客搭建已经有一阵了，但一直采用的默认的主题，没时间更换。今天特意抽时间来更换下，先上[Octopress官网](http://octopress.org/docs/theme/)了解了下更换Theme的原理，然后上Octopress所在的源码托管平台GitHub，在其[Wiki](https://github.com/imathis/octopress/wiki)上找到了[第三方Themes](https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes),便从前到后大致将各种themes都预览了一遍，最后选择了[Greyshade主题](https://github.com/shashankmehta/greyshade),安装方法官网写的已经非常详细，这里再啰嗦一遍：

###Install
```
$ cd octopress  #octopress directory
$ git clone git@github.com:shashankmehta/greyshade.git .themes/greyshade
$ echo "\$greyshade: color;" >> sass/custom/_colors.scss //Substitue 'color' with your highlight color
$ rake "install[greyshade]"
$ rake generate
```
至此，安装过程便已完成。

左侧的显示效果主要配置在_config.yml文件中。

###pages显示

Octopress默认只有Homepage和Archives两个导航菜单，不满足要求，我便又添加了"编程"、“Linux”、“所思所想”和“关于我”这几个。“关于我”的页面为静态页面，在source/blog/aboutme/下，其他的几个需要将相关的文章显示在相应的导航菜单下，便需做如下配置：

```html source/thinking/index.markdown
---
layout: category_index
title: Thinking
category: Thinking
---
```
这样后，只要new_post并且category为Thinking的页面都会集中在所思所想对应的页面显示。


