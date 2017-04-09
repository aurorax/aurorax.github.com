title: Android手机无法连接VPN
tags:
  - android
  - vpn
  - 权限
id: 359
categories:
  - Code
date: 2012-12-28 10:28:36
---

这个问题困扰我一段时间了，起初认为是vpn的问题，后来在网上搜索才知道是手机权限设置问题。
修复需要root权限，一般也是在手机root之后会出现类似问题。
使用文件管理器（例如Root Explorer），首先确定文件管理器的权限为“R/W”，然后进入/etc/ppp文件夹，设置其中ip-up-vpn权限为777（全打上对勾）即可。