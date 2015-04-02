---
layout: post
title: "ASP.NET MVC Json()处理大数据异常解决方法"
date: 2013-09-26 15:15
comments: true
categories: [ASP.NET, Thinking]
---

近几天一直忙于windows下的项目，rails的学习暂时搁置了，所以也有好几天没有用fedora了，博客大致也有一周没有更新。此博客本想只记录一些Linux平台下的相关操作，但这两天碰到的问题很棘手，虽最终得以解决，但不忍就此翻篇，想将解决之法记录下来，以避免今后再次碰到此类问题又得重头再寻求解决方案，同时也分享出来，避免其他人碰到此问题时多走弯路。所以便予以记录。下面切入正题：

先对项目做个简单介绍：

<!-- more -->

整个项目采用微软的ASP.NET MVC3进行开发，前端显示采用EasyUI框架，图表的显示用的是Highcharts，主要进行曲线图的绘制，这样比较形象地描绘出变化的趋势。由于数据量比较大(大于1000，000条记录)，而highcharts接受的数据类型为json格式，所以controller从数据库中取出的数据需要先格式化成json,然后再传到前端。平时一直采用MVC的Json()将数据序列化成json格式，但是由于此次数据量较大，所以曲线不显示，所以一直以为是由于数据量较大，highcharts插件不支持100w级数据，后来听人说highcharts本身是支持100w级数据的。最后采用firebug调试才发现出现了错误：“使用JSON JavaScriptSerializer进行序列化或反序列化时出错。字符串的长度超过了为maxJsonLength属性设置的值”,网上也找了不少解决方案，几乎无一例外说的是在web.config的<configuration>节点下添加：

	<system.web.extensions>
		<scripting>
			<webServices>
				<jsonSerialization maxJsonLength="1024000000" />
			</webServices>
		</scripting>
	</system.web.extensions>

试过后发现曲线还是没出来，最后拿出杀手锏：谷歌翻译成英文，再次搜索，最后终于在stackoverflow上找到解决之法：

	public ActionResult GetLargeJsonResult()
	{
	  return new ContentResult
		{
			Content = new JavaScriptSerializer { MaxJsonLength = Int32.MaxValue }.Serialize(myBigdata),
			ContentType = "application/json"
		};
	}

具体网址：http://stackoverflow.com/questions/4155014/json-asp-net-mvc-maxjsonlength-exception

这里不得不大赞StackOverflow,好多问题都是在上面找到solution,而且上面还有非常多的好心人士热心细致的回答问题，我提了好几个问题都最终得到所谓Geek的帮助并得以解决。这里，我只想说声：谢谢。


