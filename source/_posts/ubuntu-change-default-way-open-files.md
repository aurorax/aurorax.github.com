title: ubuntu14.04修改文件的默认打开方式
tags:
  - '14.04'
  - ubuntu
  - 打开
  - 文件
  - 默认
id: 822
categories:
  - Ubuntu
date: 2014-11-23 12:50:51
---

在ubuntu中默认的文本文档打开方式是gedit，想更换为eclipse。
首先确认/usr/share/applications下是否有eclipse.desktop文件，若没有创建。

	$ vim eclipse.desktop
	
键入

	[Desktop Entry]
	Type=Application
	Name=Eclipse
	Comment=Eclipse Integrated Development Environment
	Icon=eclipse
	Exec=eclipse
	Terminal=false
	Categories=Development;IDE;Java;
	
保存退出。
14.04默认界面为gnome，则修改gnome下的default.list

	$ vim /etc/gnome/default.list
	
找到

	text/plain=gedit.desktop
	
这是默认文本文件的设置项，修改为

	text/plain=eclipse.desktop
	
保存退出即可。
若遇到图标不正常，修改eclipse.desktop中Icon项，使其指向eclipse图标

	Icon=/usr/share/pixmaps/eclipse.png
	
若不能正常打开eclipse，修改eclipse.desktop中Exec项，使其指向eclipse执行文件

	Exec=/usr/bin/eclipse