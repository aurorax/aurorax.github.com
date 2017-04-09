title: Ubuntu打开pdf文件中文无法正常显示
tags:
  - pdf
  - ubuntu
  - 中文
  - 无法
  - 横线
  - 正常显示
  - 空白
id: 590
categories:
  - Ubuntu
date: 2013-10-26 12:14:07
---

Ubuntu下打开PDF文档后，无论用何种阅读软件，都无法正常显示，显示空白和横线。Google了一下，找到解决方法。

	$ sudo apt-get install poppler-data
	
完成安装后，就可以正常显示中文了。