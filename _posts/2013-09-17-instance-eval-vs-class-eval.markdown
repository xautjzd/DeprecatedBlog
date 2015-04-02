---
layout: post
title: "instance_eval vs class_eval"
date: 2013-09-17 20:54
comments: true
categories: Ruby
---
Ruby中类其实也是Class的实例。而且instance_eval必须由实例来调用，class_eval必须由类来调用。具体参考下面的实例：

```ruby
	class A
	end

	a = new A
	a.instance_eval do
		self #=>a
		
		def test
			puts "this is a singleton method of instance a"
		end
	end

	a.test   #=>this is a singleton method of instance a

	b = A.new
	b.test   #=>NoMethodError
```

<!-- more -->

test的receiver为实例a.同时类A本身也是Class类的实例，所以也可以作为instance_eval的receiver，作为该类的singleton method，及常说的类方法，只能通过类名调用。

```ruby
	class A
	end

	A.instance_eval do
		def test
			puts "this is a singleton method of class A"
		end
	end

	A.test  #=>this is ...
```

而class_eval则receiver则必须为类

```ruby
	class A
	end

	A.class_eval do
		self  #=>A

		def test
			puts "this is a instance method of class A"
		end
	end

	a = new A
	a.test   #=>this is a instance method of class A
```

class_eval定义的method为类的instance method。

这就是它们二者之间的差别
