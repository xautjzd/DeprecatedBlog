---
layout: post
title: "Hadoop集群"
date: 2013-10-22 20:51
comments: true
categories: Linux
---
最近开始研究起Hadoop,《Hadoop in Action》大概看了3章，然后开始着手搭建环境。

由于设备的受限，让老师给分了两台虚拟机（4G内存，20G硬盘，CentOS6.4），在上面开始搭建Hadoop集群，其中一台作为master,另一台作为slave。环境的搭建大概花了一天多的时间，主要有JDK的配置和SSH的配置，这两项已经是轻车熟路，所以很快便配置好。但是Hadoop才刚接触，所以配置起来速度慢点，没有一个绝对的参考资料，网上资料虽颇丰，但甄别对与错却需要一定时间，并且还要弄懂配置参数的意义。前后大致花了有半天时间。配置好后启动服务时却出错，google搜索了好久，也试过很多方法，但一直没解决。

<!-- more -->

问题主要出现在权限这块，因为采用root启动服务没问题，但是一般用户启动便提示创建`/var/logs/user`出错，权限不够，而我的logs目录已经在`conf/hadoop-env.sh`中设置为hadoop解压目录下的logs目录。最后实在没辙，便尝试重新配置。大致步骤也是按前边的进行，但是没想到最后竟然成功，真的太让人意外！通过jps能够看到master的namnode,jobtracker等的进程号，同时也能在slave上看到datanode,tasktracker的进程号。

安装好后，当然得找个实例测试下，hadoop的解压目录下自带有example，其中有个wordcount,便拿来测试了。

### 创建本地测试文件

	$mkdir ~/file
	$cd ~/file
	$echo "Hello World" >> ~/file1.txt
	$echo "Hello Hadoop" >> ~/file2.txt

### 在HDFS上创建Input目录

	$hadoop fs -mkdir input
	$hadoop fs -ls

### 导入本地测试文件到HDFS中的input目录

	$hadoop fs -put ~/file/file*.txt input
	$hadoop fs -ls input

### 运行wordcount程序

以input为输入目录，output为输出目录

	$hadoop jar ~/hadoop-1.2.1/hadoop-examples-1.2.1.jar wordcount input output
	
### 查看结果

运行的结果会保存在output下的part-r-00000文件中，查看方法如下：

	$hadoop fs -cat output/part-r-00000

### 后话

近两天在看龙应台女士的《亲爱的安德烈》一书，全书以书信的方式来展开，通过她与儿子安德烈的对话，了解了香港、台湾及德国的一种生活方式，尤其是香港人民2005年的游行，不禁让我想到了中国的现状，顿时有种压抑的感觉，感觉中国人民一直在努力的奋斗，无非就是为了一份安宁的生活。但感觉就是这么一份安宁，却让太多的人为之奋斗一生而不得或千辛万苦才得，突然觉得这样的人生还有意义么？我目前期望的仅是今后能生活在技术圈中，而且不用再被生活所奴役，不愿再面对一群不懂技术而趾高气扬的人，已经听到身边不少人羡慕国企、银行、研究所等铁饭碗的单位，但我却丝毫没有兴趣，因为在我印象中，那些单位大多给人一种散漫感，其中充满了太多的勾心斗角，尔虞我诈，而我本身却非常厌恶这些，真的可以说让人作呕。呆在这样的环境工作一生，想想都觉得枯燥无味。希望明年能找到一份理想的工作，干自己喜欢的技术。
