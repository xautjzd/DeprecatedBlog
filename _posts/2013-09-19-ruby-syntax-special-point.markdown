---
layout: post
title: "Ruby语言独特点"
date: 2013-09-19 09:05
comments: true
categories: Ruby
---
有时候真佩服别人的博文可以写的那么长，而且很有料，读起来也非常顺畅，而自己每次却不太善于总结，可能是平时积累的片段还不够，不足以总结，亦或是自己缺少这么一个总结性的思维，导致如今为止也没有产出一篇广为阅读的文章。不过即使如此，也没有打消我持续写博客的念头，不管好坏，不管是否有读者，我将会一如既往的写下去。正如哥哥的《我》:我就是我，是颜色不一样的烟火。每个人都有他存在的价值，无论高低贵贱，无论贫穷富贵，都有其独一无二不可替代的特性。所以无论自己的博文是否能带给大家一丝感触、一点帮助，我都会坚持，因为这也是对我自己学习的一个总结，同时也想尽力贡献一份自己的力量来帮助他人，但我想更多的还是能帮助自己，以便为未来某一天突然需要回味从前的知识提供便捷。我想这便是写博客的初衷。下面进入正题吧：

<!-- more -->

##无须声明变量

Ruby第一个独特之处我想应该是定义变量时无须指定变量类型吧。eg:

	time = Time.now
	i = 1
	text = "hello,world"

虽说变量定义时无类型，但是当为其赋值后类型便确定了。

##一切皆对象

另一个特点应该非`一切皆对象`莫属了，即使是简单的变量也是一个对象，可通过class方法查看其类型：

	1.class           #=>Fixnum
	1.1.class         #=>Float
	"test".class      #=>String
	[].class          #=>Array
	{}.class          #=>Hash

##Mixin

而Mixin应该算是其第三个独特之处，通过在Class中mixin Module以达到类似c++里面的多重继承吧，虽然ruby中没有多重继承这个概念。eg:

	module Hello
		def say_hello
		 puts "hello!"
		end
	end

	class TestClass
		include Hello
	end

这样TestClass即使内容为空，但因为有Hello的mixin，所以也拥有say_hello方法。

##yield

yield真的是Ruby的一大亮点，也是我所学所了解的语言当中最独特的部分，同时也是我深爱Ruby的原因。yield通俗的讲其实就是一个占位符，提前帮block占好位置。block可以再程序运行的时候动态传给方法。eg:

	class Test
		@data = [1, 2, 3, 4]

		def test
			if block_given?
				@data.each { |e| yield(e) }
			else
				puts "please give block"
			end
		end
	end

	obj = Test.new
	obj.test { |x| puts x*x }  #=>1, 4, 9, 16

定义时可以不指定具体操作，先用yield占位，然后待到具体操作时，将具体处理的block传入方法。

##写在结尾的话

自己断断续续学习Ruby大致也不到一年时光，所以理解也不是很深入，只将我自己所理解的所看到的所学到的列举出来。其实自己也看过《Meta Programming》，深深为method_missing，eval等所折服，但是还是理解不到家，所以也不敢妄自胡言乱语，以免贻笑大方。深入的东西留待后续的学习吧。

