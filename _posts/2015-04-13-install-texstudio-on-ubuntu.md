---
layout: post
title: "Ubuntu安装TexStudio"
description: ""
category: Tech
tags: [LaTex]
---

![](/images/20150601.png)

自从去年简历采用LaTex制作后,便逐渐对它有了好感.不过当时用的是Windows环境,直接采用Windows下的套装CTex进行简历的编辑与PDF的生成,编辑器采用的Texworks,且简历的模板还是网上宕下来并小作修改.虽然成功地生成简历,不过源码里面的不少细节还是一知半解.后来换到Ubuntu环境,又成功安装Linux下的LaTex编译环境[Texlive][1],不过Texlive提供的只是编译环境而已,需要自己找寻称手的编辑器采用tex语法编辑好文档后并保存成`.tex`格式文件,然后采用texlive的编译幻镜进行编译.由于自己是Vim党,所以从一开始便试图采用Vim进行tex文档编辑,试了好几个Vim下的LaTex插件,都未能称心.我的需求大致如下:

<!-- more -->

- 标签自动补全(必要)

直到有一天在好友胡俊的推荐下获知TexStudio的存在,便尝试了下，发现确实相当不错。不仅提供了GUI的界面，使操作变得更为方面，而且还有标签自动补全等功能。只是发现默认安装后中文编译乱码。查阅了一些文档，得知TexStudio其实是**依赖texlive**的，底层的编译器如pdflatex等还是texlive的，宏包也是依赖texlive。所以要想顺利使用TexStudio，还是得先安装texlive,为了添加中文的支持，需要采用texlive提供的包管理工具安装中文相关的宏包。

下面为安装完成后的测试代码：

{% highlight tex linenos %}
    \documentclass{article}
    \usepackage{CJKutf8}
    \title{hello}
    \author{xautjzd}

    \begin{document}
        \maketitle
        \begin{CJK}{UTF8}{gbsn}
            宋体中文测试
        \end{CJK}
        \begin{CJK}{UTF8}{gkai}
            宋体中文测试
        \end{CJK}
    \end{document}
{% endhighlight %}

效果如下图所示：
![](/images/20150601-latex.png)

[1]: http://tug.org/texlive/
