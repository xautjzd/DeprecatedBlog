---
layout: post
title: "更新Octopress"
date: 2013-09-17 15:22
comments: true
categories: Octopress
---

现在已记不清接触Octopress多长时间了，只依稀记得当时配置Octopress配了好久，然后依然失败，后又忙于其他的事情，所以搭建工作便搁置一旁，七月中旬时间比较充足，所以又开始再次折腾，后来终于搭建成功，所以7.18便发表了第一篇博客。后来一个月之后又开始了我的换肤工作，一切都好，唯一的缺陷是Gravatar的图像没有显示出来，所以便向theme的作者发问，后来也忘了这茬事。就这样又过了一月，直到今天，突然发现我的unread消息里面有几条关于我的message，便打开浏览，才发现作者给的回复，说图像没显示是个bug，现已修复。具体见：

https://github.com/shashankmehta/greyshade/issues/42

我便立马更新了我的Octopress。更新方法如下：
 
	# Get the latest Octopress
	git pull octopress master    
	# Keep gems updated
	bundle install               
	# update the template's source
	rake update_source            

具体参考：

http://octopress.org/docs/updating/

参考时请务必注意：如果您的octopress主题不是octopress默认主题,请不要执行`rake update_style`，否则会被还原成默认主题。


本博客采用的主题为：

https://github.com/shashankmehta/greyshade

