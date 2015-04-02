---
layout: post
title: "Ocpress添加友情链接"
date: 2013-07-27 16:02
comments: true
categories: Octopress
---
与在侧边栏添加Aboutme、Categories、Tagcloud等功能类似，在source/\_include\custom\asides目录下添加一个frendsites.html文件，模仿about等写法，添加友情链接，如下所示：

```html
    <section>
        <h1>友情链接</h1>
        <ul>
            <li><a href="url_to_add">友情链接的显示Id</a></li>
            ...
        </ul>
    </section>
```

然后在\_config.yml文件中相应的位置添加，如在default\_asides中的数组添加custom/asides/friendsites.html，当然也可以在blog\_index等其他数组中添加。
