title: raspberry pi在ubuntu/linux下的系统烧录
tags:
  - linux
  - pi
  - raspberry
  - sd
  - ubuntu
  - win32diskimager
  - 烧录
id: 644
categories:
  - Ubuntu
date: 2013-11-09 10:16:26
---

上一个raspberry pi是在windows下烧写的，用的是图形工具，有很明显的进度提示，这次尝试ubuntu下使用命令行写入，相较于windows图形界面略为繁琐。
首先还是要下载镜像：[http://www.raspberrypi.org/downloads](http://www.raspberrypi.org/downloads)
我选择的是raspbian：[http://downloads.raspberrypi.org/raspbian_latest](http://downloads.raspberrypi.org/raspbian_latest)
下载完成后解压，然后启动命令行，在确保sd卡正确插入的前提下，运行命令

	$ df -h
	
会看到文件系统的挂载，找到容量与你的sd卡相当的挂载点，例如我的

	/dev/sdc1 7.4G 32K 7.4G 1% /media/3539-6535
	
记下挂载点，然后cd到镜像所在的目录，找到刚刚解压的镜像名，例如我的是

	2013-09-25-wheezy-raspbian.img
	
然后需要卸载挂载点，使得用户对不能对sd卡数据进行操作

	$ umount /dev/sdc1
	
运行

	$ sudo dd if=2013-09-25-wheezy-raspbian.img if=/dev/sdc1 bs=2M
	
其中: if = Input File, of = Output File, bs = Block Size
bs可以为4M，比2M更快，但是对于某些sd卡会出问题，所以换为2M，如果2M也有问题就换为1M，但是会更慢
如果你的系统是中文运行上述dd命令后会呼呼的跑乱码，据说英文系统会正常？不得考证，但是命令行下是不会有进度提示的，甚至到后面复制文件的时候连乱码都没有，你会以为程序死掉了，但其实后台实在复制文件的，可以重新开一个命令行窗口，使用这个命令查看复制进度

	$ sudo pkill -USR1 -n -x dd
	
进度会显示在第一个运行dd的窗口
理论上讲，等到命令运行结束，你的sd卡就烧好了，但是我不得不换用windows下的[Win32DiskImager](http://sourceforge.net/projects/win32diskimager)，因为命令行实在是太慢了，等待了半个小时后我实在受不了了，并且ubuntu下的图形界面貌似有bug：[https://bugs.launchpad.net/usb-imagewriter/+bug/1013834](https://bugs.launchpad.net/usb-imagewriter/+bug/1013834)
最后一段还没有写完，win下的sd烧录已经完成了。
Have fun～