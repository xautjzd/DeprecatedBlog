---
layout: post
title: "账号注册通过邮箱激活"
date: 2013-09-03 21:48
comments: true
categories: [Thinking] 
---
### 邮箱激活目的

防止用户注册时所填写的信息为虚假信息

### 邮箱激活的原理

用户注册时，根据用户名、Email及注册时间(精确到ms)等信息通过特定的算法(如:MD5、SHA，最好不可逆)生成相应的信息摘要(也称消息摘要)作为注册的激活码，保存到数据库当中，并且将其作为url的参数，将带有激活码的url链接发送到用户注册的Email中。

只有当用户进入邮箱中并点击该链接后，通过url中的激活码找出数据库中匹配的用户，并将此账号设为“已激活”的状态。

**注：此过程没有考虑激活码过期问题，同时信息摘要也可以通过随机数来表示，不一定非要通过用户名等信息生成**

Rails代码参考：

[http://stackoverflow.com/questions/12805523/activate-user-via-email-in-rails](http://stackoverflow.com/questions/12805523/activate-user-via-email-in-rails)




