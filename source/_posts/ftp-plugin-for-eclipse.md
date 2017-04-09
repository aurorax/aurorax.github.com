title: eclipse添加ftp插件
tags:
  - eclipse
  - ftp
  - plugin
  - 插件
id: 594
categories:
  - Code
date: 2013-10-28 12:45:15
---

做php开发经常需要对服务器文件进行实时修改，所以Eclipse的ftp插件必不可少。
eclipse内建的插件是"Remote System Explorer End-User Runtime"，支持ftp和ssh，我的eclipse是英文版，不同的版本在名称上可能会有所差别，但大概是相同的。
菜单栏点击'Help'->'Install New Software...'，在'Work with:'中添加eclipse版本对应发布站的地址，例如我的版本是Indigo，则输入：Indigo - http://download.eclipse.org/releases/indigo/
然后在下面的filter输入框输入'remote'，在搜索出来的'Remote System Explorer End-User Runtime'前面打对勾，然后'Next'就会开始安装了。
安装结束后会要求重启eclipse，重启完毕后点击'Window' -> 'Open Perspective'，如果找不到'Remote System Explorer'就选择'Other'，在弹出的对话框中选择'Remote System Explorer'，左边就会出现'Remote Systems'的边栏，点击第一行的第一个按钮，也就是添加按钮，选择'FTP Only'->'Next'，弹出的对话框中'Host Name'填写FTP的地址，然后'Finish'就可以了，用户名密码会在后面填写。
现在'Remote Systems'边栏中会出现刚刚添加的ftp，选中后单击右键选择'Connect'就会出现填写用户名密码的对话框，填好以后'OK'，记得选中'Save Password'，否则每次connect都要填密码。
至此FTP链接就完成了，稍等一会读取目录，可以进行文件操作了。