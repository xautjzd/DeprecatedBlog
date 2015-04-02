---
layout: post
title: "Git远程分支的一些操作"
date: 2014-04-01 08:52
comments: true
categories: [Linux, Git]
---

![](/images/20140401.jpg)

我是个爱折腾的人，昨天晚上突然看着自己的博客主题不爽，便立马将其从原先的Greyshade换到现在的Cleanpress。换完并构思一篇新博客之后，再次提交到GitHub上，得到提示此分支滞后于GitHub上，采用`git pull`又产生了太多冲突，冲突少手动解决还可，太多更改起来太麻烦，便萌生推掉远程分支重新提交的念头。可之前从未对远程分支做过相关的操作，只是偶尔删除远程库上的单个文件而已，又不得不求助Google了。碰到问题在解决过程中总是会学到很多，并且记忆深刻，现予以记录，方便自己，也回馈社会。

删除之前先查看远程分支，在确定的情况下再作删除，以致不会删错。

## 查看远程分支

采用`git branch -a`可查看所有的分支(本地+远程),而`git branch -r`仅显示远程。如果打开颜色支持，还会看到远程分支的颜色与本地不同。

<!-- more -->

```
$git branch -a
* newtheme
  source
  remotes/origin/HEAD -> origin/master
  remotes/origin/newtheme
  remotes/origin/source

```

## 删除远程分支

```
$git push origin --delete <branchname>
```
删除tag也是同样的操作：

```
$git push origin --delete <tagname> 
```

由于我删除的是远程库的默认分支master,所以在删除过程中产生了以下错误：

```
remote: error: refusing to delete the current branch: refs/heads/master
To git@github.com:xautjzd/xautjzd.github.com.git
 ! [remote rejected] master (deletion of the current branch prohibited)
	error: failed to push some refs to 'git@github.com:xautjzd/xautjzd.github.com.git'

```

这时只要进入该项目的settings，将default branch改为其他分支便可进行删除工作。

## 重命名远程分支

将本地分支推送到一个不存在的远程分支上便可新建远程分支，推送过后发现名称不对，便可通过下面的命令来修改名称：

```
$git branch -m oldname newname
```
