title: 'vmware:正在尝试加载64位应用程序，但此cpu与64位模式不兼容'
tags:
  - 64bit
  - 64位
  - bios
  - Intel Virtualization Technology
  - vmware
  - windows7
  - 不兼容
id: 651
categories:
  - Ubuntu
date: 2013-11-17 17:12:59
---

我是在ubuntu下使用vmware安装windows7x64时出现这个问题的。
如果出现类似问题，有可能是cpu不是64位，或者安装的系统不是64位。
在我这里是因为cpu没有开启虚拟化，需要在BIOS里设置，没法截图，照相嫌麻烦。
设置项叫做：Intel Virtualization Technology
有些主板在“Config”标签下，有些在“Secure”下，BIOS里面没几页，如果找不到就是cpu不支持虚拟化。
把“Intel Virtualization Technology”这一项设置为“Enable”，再运行vmware就正常了。