---
layout: post
title: "vim-airline插件patched font配置成功"
date: 2013-08-26 11:30
comments: true
categories: [Vim,Linux]
---
前段时间装好了airline插件，但是没呈现应有的效果，原因是没有安装字体。根据官网的提示需要安装powerline的字体，我便照着[powerline官网](ttps://powerline.readthedocs.org/en/latest/installation/linux.html#font-installation)的配置方法来，但是还是没有成功。其原因是我安装了patched fonts，但是没有将terminal的font设置为patched fonts中的一种，所以statusbar会有乱码。下面对安装patched fonts做一个小结。

安装patched fonts方式请参考:[powerline字体配置](https://powerline.readthedocs.org/en/latest/installation/linux.html#font-installation)，尽管文档很详细，但是还是重复一下：

1.Download patched fonts

`$mkdir ~/.fonts`新建一个font文件夹，然后`$cd ~/.fonts`进入.fonts文件夹。`$git clone git@github.com:Lokaltog/powerline-fonts.git`将powerline的patched fonts拷贝到~/.fonts目录下，目录结构如下图：

![~/.font目录结构](http://pic.yupoo.com/xautjzd/D79oXi6w/medish.jpg)

2.Install the patched fonts to your System

运行`$fc-cache -vf ~/.fonts`安装patched fonts到系统中

3.Set Terminal fonts

设置Terminal字体非常重要，我初次配置时，安装patched fonts，但是由于没有set terminal font,所以statusbar显示乱码。设置方法如下：

Edit——Profiles——Default(Edit)——General——Font，选择~/.fonts/powerline下的某一种即可(可选范围一定要在刚才下载的patched fonts中选一种，否则乱码。)，当然也可以采取powerline font installing中的另一种方式，不过我没做尝试，有兴趣的朋友try it。配置截图如下：

![Font config](http://pic.yupoo.com/xautjzd/D79olvGa/medish.jpg)

最后可以在~/.vimrc中更改airline的theme。更改方式如下：

	let g:airline_theme="molokai"

