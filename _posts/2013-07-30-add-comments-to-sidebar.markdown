---
layout: post
title: "Octopress添加disqus评论到侧边栏"
date: 2013-07-30 10:47
comments: true
categories: Octopress
---

##新建comments.html文件

添加评论到侧边栏与添加关于、文章分类和友情链接相似，需要在source/\_includes/custom/asides/目录下添加comments.html模块，名字根据自己的喜好可以换成其他的，如xxx.html，然后在comments.html里添加如下内容：

```html
<section id="comment_sidebar">
	<h1>近期评论</h1>

	<script type="text/javascript" src="http://zhengdongjiang.disqus.com/recent_comments_widget.js?num_items=5&hide_avatars=0&avatar_size=32&excerpt_length=20"></script><a href="http://disqus.com/">Powered by Disqus</a>
</section>
```

其中zhengdongjiang为我disqus对应此网站的shortname，这就不要照搬了，换成你对应的名字即可。

##修改_config.yml文件

```
	default_asides: [custom/asides/category_list.html, asides/recent_posts.html, custom/asides/comments.html, custom/asides/friend_sites.html, asides/pinboard.html]

	# Each layout uses the default asides, but they can have their own asides instead. Simply uncomment the lines below
	# and add an array with the asides you want to use.
	blog_index_asides: [custom/asides/about.html, custom/asides/category_list.html, asides/recent_posts.html, custom/asides/comments.html, custom/asides/friend_sites.html, asides/pinboard.html]
	post_asides: [custom/asides/about.html, custom/asides/category_list.html, asides/recent_posts.html, custom/asides/comments.html, custom/asides/friend_sites.html, asides/pinboard.html]
```
