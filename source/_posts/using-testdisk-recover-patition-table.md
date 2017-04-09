title: 使用TestDisk恢复分区表
tags:
  - clean
  - disk
  - diskpart
  - test
  - testdisk
  - 分区表
  - 恢复
id: 803
categories:
  - Ubuntu
date: 2014-09-09 20:55:50
---

比较悲催的一件事。
不小心在Diskpart里使用了clean命令，分区不见了...
查了一下，这个只是删除了分区表，分区信息还在，所以不要紧张。
找个空U盘，用另一台功能正常的机器写入老毛桃PE，老毛桃更新到现在已经非常简单，几乎是一键写入，注意看清楚盘符。
然后下载TestDisk:
[http://www.cgsecurity.org/wiki/TestDisk_Download](http://www.cgsecurity.org/wiki/TestDisk_Download)
这是一个大神级开源软件，支持多平台，对各种类型分区都能良好识别。
对于老毛桃PE，下载win平台版本即可，解压后放入写好的U盘。
设置BIOS使用U盘启动后，打开"testdisk_win.exe"，进入命令行界面。
选择

	[ Create ] Create a new log file
	
然后根据容量和品牌判断需要恢复的硬盘，如果你有两块的话。然后

	[ Proceed ]
	
然后选择具体的分区表类型，程序会自动判断可能存在的分区表类型，显示在下方"Hint"后面，如何不太清楚，直接选择程序自动判断的类型即可。
然后

	[ Analyse ] Analyse current partition structure and search for lost partitions

回车以后选择

	[ Quick Search ]

程序会搜索出所有的分区，按照分区类型和大小来判断分区类型，用左右方向键调整主分区，逻辑分区和启动分区（如果有的话），直到所有的横条都变成绿色，即可回车继续。
然后使用方向键选择

	[ Write ]

写入，分区表的恢复就完成了。