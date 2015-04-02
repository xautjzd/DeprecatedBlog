---
layout: post
title: "Git的相关操作"
date: 2013-07-22 11:33
comments: true
categories: Git 
---

##查看Git远程库地址
建立了远程库后，许久没操作，突然忘了其对应的具体远程库的url。可通过以下命令来查看：

    $git remote -v

-v选项是--verbose的简写，最后结果为：

    origin git@github.com:xautjzd/RubyExample.git (fetch)  
    origin git@github.com:xautjzd/RubyExample.git (push)

要查看详细信息，则可以通过如下命令查看：

    $git remote show remote-name

##添加远程库地址
    $git remote add reponame url

##远程库的重命名
    $git remote rename oldname newname

<!-- more -->

##删除远程库
    $git remote rm remote-name

##恢复git reset --hard误操作
使用git类的版本控制器一定要谨慎，因为通常涉及版本控制器的管理都是重要文档，不容有失。特别是涉及reset、rebase、checkout和merge等一些高级操作时，更要格外小心。

当然总是难免会有误操作，而通常伟大的工具都会有误操作的恢复功能。首先可以通过git log查看提交日志。然后查看上次提交的commitid,通过git reset --hard commitid可以将暂存区和工作区替换成某个点的repository。这样可能新添加到工作区的文件会丢失，不过不用担心，如果想还原，则通过：
    $git reflog     #reflog记录着所有的HEAD历史
    $git reset --hard commitid   ##回滚到某次HEAD

短时间内可以回滚,如果长时间，则可能记录会被git当作垃圾清理掉。
