---
layout: post
title: "Cookies vs Sessions"
date: 2013-09-09 10:37
comments: true
categories: [Thinking]
---
Http是无状态的协议，客户端给服务器发送请求，服务端响应客户端的请求，会话结束。这样两次会话间不便没有任何关联。但有时候需要在会话间进行信息共享，如：购物车，保存用户名与密码等。为此，cookie与session便诞生了,它们的存在就是为了弥补http协议无状态的缺陷。

cookie与session最大的不同是：cookie保存在用户的浏览器中，而session则保留在服务端。正是这种不同决定了它们的不用使用场合。

##Cookie
---

cookie机制是通过扩展http协议来实现的。服务器通过在HTTP的响应头中加上一行特殊的指示以提示浏览器按照指示生成相应的cookie。其实纯粹的客户端脚本如JavaScript或者VBScript也可以生成cookie。而cookie的使用是由浏览器按照一定的原则在后台自动发送给服务器端。

cookie主要内容包括：Name,Content,Path,Domain,Expires(过期时间)等。Domain与Path一起构成cookie的作用范围。

若不设置Expires,则默认的cookie生命周期为浏览器会话期间，一旦浏览器关闭，cookie则会被清理掉，这种生命周期为浏览器会话期的cookie被成为会话cookie。会话cookie存储在内存中而不是在硬盘上。

若设置了Expires,浏览器则会把生成的cookie保存在硬盘上，即使浏览器关闭后再打开，cookie依然有效，直至超过设置的expires。

另外，session大小有限制，一旦浏览器禁用cookie，则采用cookie的购物网站便不能进行购物，所以这时候得用session了。

<!-- more -->

##Session
---

session机制是一种服务器端的机制，服务器使用一种类似于散列表的结构（也可能就是使用散列表）来保存信息。

当程序需要为某个客户端的请求创建一个session时，服务器首先检查这个客户端的请求里是否已包含了一个session标识（称为session id），如果已包含则说明以前已经为此客户端创建过session，服务器就按照session id把这个session检索出来使用（检索不到，会新建一个），如果客户端请求不包含session id，则为此客户端创建一个session并生成一个与此session相关联的session id，session id的值应该是一个既不会重复，又不容易被找到规律以仿造的字符串，这个session id将被在本次响应中返回给客户端保存。保存这个session id的方式可以采用cookie，这样在交互过程中浏览器可以自动的按照规则把这个标识发送给服务器。一般这个cookie的名字都是类似于SEEESIONID。但cookie可以被人为的禁止，则必须有其他机制以便在cookie被禁止时仍然能够把session id传递回服务器。

经常被使用的一种技术叫做URL重写，就是把session id直接附加在URL路径的后面。还有一种技术叫做表单隐藏字段。就是服务器会自动修改表单，添加一个隐藏字段，以便在表单提交时能够把session id传递回服务器。

##Cookie与Session区别
---

1. cookie存储在客户端的浏览器中，而session则存储在服务器上。
2. cookie不安全，可以通过分析本地cookie并进行cookie欺骗，而session则相对比较安全。
3. session会在服务器上保存一段时间，但当访问量增大，会占用服务器的存储空间，影响服务器的性能，如考虑到减轻服务器的性能，则可以选择cookie。
4. 单个cookie保存的数据不会超过4k。

所以，一般将登陆等重要信息采用session保存，而其他信息则采用cookie。

##参考资料
---
1. http://en.wikipedia.org/wiki/Session_(computer_science)
2. http://en.wikipedia.org/wiki/HTTP_cookie#cite_note-1
3. http://www.cnblogs.com/shiyangxt/articles/1305506.html
