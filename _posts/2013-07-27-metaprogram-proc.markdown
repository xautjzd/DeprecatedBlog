---
layout: post
title: "Ruby元编程之Proc对象"
date: 2013-07-27 12:40
comments: true
categories: Ruby
---
## Proc 

Proc对象其实就是将代码块(block)转换成对象的块。方式有大致几种：

1.Proc对象

```ruby
    inc = Proc.new{ |x| x + 1 }
    inc.call(3)     #=>4
```

2.lambda方法

```ruby
    inc = lambda{ |x| x + 1 }
    inc.call(3)     #=>4
```

<!-- more -->

3.proc方法

```ruby
    inc = proc { |x| x + 1 }
    inc.call(3)     #=>4
```

## &操作符

块就如同方法的额外的匿名参数。大部分情况下，在方法中可以通过yield语句直接运行一个块。但是在下面两种方法中yield则无能为力了:

- 将块传递给另一个方法
- 将块转换为Proc对象

为了应付这两种情况，则需要将块附加到一个绑定上，通过给方法加一个特殊的参数便可实现，但这个参数必须为参数列表的最后一个，且以&符号开头。如下：

```ruby
    def math(a, b)
        yield(a, b)
    end

    def teach_math(a, b, &operation)
        puts "Let's do the math:"
        puts math(a, b, &operation)
    end

    teach_math(2, 3){ |x, y| x * y }   #=>Let's do the math:6
```

其实&真正的含义是：

这是一个Proc对象，我想把它当成一个块来使用，简单地去掉&操作符，就能再次得到一个Proc对象。
