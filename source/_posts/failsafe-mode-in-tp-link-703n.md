title: openwrt:tp-link 703n v1.6 failsafe模式
tags:
  - tp-link
  - 703n
  - v1.6
  - openwrt
  - failsafe
  - reset
id: 883
categories:
  - Openwrt
date: 2015-06-06 00:31:39
---

刚搬家不久，拿出来很久不玩的703n，放门厅给卫生间提供wifi信号（新房子布局很奇葩），手贱把lan和wan的地址改成一样的了...

然后就是翻openwrt：
[http://wiki.openwrt.org/zh-cn/toh/tp-link/tl-wr703n#failsafe_mode](http://wiki.openwrt.org/zh-cn/toh/tp-link/tl-wr703n#failsafe_mode)
我的版本是v1.6，开机等待亮灯迅速按reset，灯快闪，即进入failsafe模式。
这里关于failsafe的wiki页面有一个地方不适用703n：
[http://wiki.openwrt.org/doc/howto/generic.failsafe](http://wiki.openwrt.org/doc/howto/generic.failsafe)
其中说灯快闪以后还要广播一个udp包，其实对于703n是不需要的。还有一个不适用703n的地方是要拔掉wan口，703n就只有一个wan口，拔掉要怎么连...wan口连好pc，pc设置固定ip段192.168.1.0/24，直接在快闪的时候就可以telnet 192.168.1.1。进入系统默认是只读的，需要

	$ mount_root
	
然后就想怎么改怎么改了。