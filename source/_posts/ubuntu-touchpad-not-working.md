title: ubuntu触摸板不能使用
tags:
  - synaptics
  - ubuntu
  - 不能识别
  - 触摸板
  - 驱动
id: 479
categories:
  - Code
date: 2013-06-17 11:03:12
---

今天起来准备为ubuntu更新软件，发现触摸板不能用了。
插上鼠标进入鼠标和触摸板设置，根本找不到触摸板标签。
谷歌一番貌似是驱动问题，ubuntu不能识别触摸板。
最初搜索到的解决办法是编辑/etc/default/grub，找到GRUB_CMDLINE_LINUX=""，更改为 GRUB_CMDLINE_LINUX="i8042.reset i8042.nomux i8042.nopnp i8042.noloop"。
然后sudo update-grub。重启。
无果，于是继续谷歌。第二个解决办法是

	$ sudo modprobe -r psmouse
	$ sudo modprobe psmouse proto=imps

触摸板是可以用了，但是在设置里还是没有出现触摸板标签。
这两句的意思大概应该是把触摸板强制识别为鼠标，但是触摸板的滑动及多点等功能还是不能使用，并且重启之后触摸板还是没有反应的，需要重新激活。
作为暂时使用的方案是可以了，但是还是不能完全解决问题。
最终的解决方案是

	$ sudo apt-get install xserver-xorg-input-synaptics

重启之后触摸板标签出来了，为什么触摸板突然不能用的原因尚不清楚，但是上面一句应该可以解决大多数问题。
ubuntu关于synaptics的wiki给出。
[http://wiki.ubuntu.org.cn/Synaptics触摸板指南](http://wiki.ubuntu.org.cn/Synaptics触摸板指南)