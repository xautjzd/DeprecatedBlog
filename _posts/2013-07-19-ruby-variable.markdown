---
layout: post
title: "Ruby基础"
date: 2013-07-19 20:33
comments: true
categories: Ruby 
---

##变量分类
- **局部变量**

一般以小写字母或下划线开头，当多个单词组成一个变量时，单词间用\_分隔。局部变量一般用在代码快里面

- **全局变量**

全局变量在整个ruby程序中都可以访问，无论他们在哪被定义。全局变量以$开头。eg:

$global\_variable = 10

- **实例变量**

实例变量的范围则是类的实例，属于某个类的实例所有，实例间相互独立。实例变量以@开头。eg:

@instance\_variable = 10

<!-- more -->

- **类变量**

类变量为所有的类实例所共有，一个实例中改变其值，另一个实例中也看到相应改变。类变量以@@开头。eg:

@@class\_variable = 10


- **类实例变量**

类实例变量只属于当前类所有，只能通过类名来访问，类的实例不能对其访问，而类变量则可以被子类及类的实例访问。

	class MyClass
  		@my_var=1
	end

##常量
常量一旦被赋值，则不能修改。以大写字母开头的标识符是常量。一般通过“模块名/类名::常量名”的形式来引用常量。eg:

```ruby
    class HelloWorld
        Version = 2.0
    end
    #access the constant
    p HelloWorld::Version   #=>"2.0"
```

第一种最直观，最易理解，缺点是改变类名时类方法需要跟着一起改，较麻烦。第三种其次，第二种时最难理解。

##类
###initialize方法
initialize方法为类的私有方法，当类调用new方法新建对象时，initialize便被调用，同时传递给new的所有实参都会传给initialize方法。
###访问方法
访问方法也就是常说的getter和setter方法，可以通过下面三种方式来定义：

- attr\_accessor:name     #定义name和name=方法
- attr\_reader:name       #定义name方法
- attr\_writer:name       #定义name=方法

###类方法
类方法的三种定义方式分别如下:  

- 第一种方式如下：

```ruby
    class HelloWorld
        def HelloWorld.hello(name)
            print "hello, ", name, "\n"     #name为局部变量
        end
    end
    HelloWorld.hello("xautjzd")     #=>hello, xautjzd
```

- 第二种方式如下：

```ruby
    class HelloWorld
        ..
    end
    class << HelloWorld
        def hello(name)
            print "hello, ", name
        end
    end
    HelloWorld.hello("xautjzd")   #=>hello, xautjzd
```

- 第三种方式如下：

```ruby
    class HelloWorld
        def self.hello(name)
            print "hello, ", name
        end
    end
    HelloWorld.hello("xautjzd")    #=>hello, xautjzd
```

###方法的访问控制
Ruby提供了三种限制方式:

+ public——默认方式，默认的实例方法都是public
+ private——private修饰的方法只能在类的内部使用，不允许在类的外部调用
+ proteced——只能在本类或者子类中访问，不能在类外部访问

##模块
模块(module)应该是Ruby特有的功能，模块中也可包含方法，成为模块方法，模块与类最大的不同在于：

- 模块不能实例化
- 模块不能继承

###模块的用法
- 提供命名空间
命名空间的存在主要是解决方法、常量、类名的冲突。使用模块时，只需要用include将模块包含进现有的命名空间中即可。eg:

```ruby
    include Math
    p Math::PI     #=>3.141592654
    p Math.sqrt(4) #=>2
```

- 以Mix-in方式提供功能
类中包含模块，成为Mix-in。eg:

```ruby
    module MyModule
        #提供的模块方法
    end

    class Class1
        include MyModule
        #Class1的方法定义
    end

    class Class2
        include MyModule
        #Class2的方法定义
    end
```

如上例所示，通过Module将Class1和Class2两个类所共有的功能抽出来定义成Module。主要用于：

* 两个类只是功能相似，但不想归于相同类型的类
* Ruby不支持多继承，所以当已继承其他父类时，就无法再继承其他的类
