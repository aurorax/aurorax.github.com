title: git使用socks代理
date: 2015-07-19 20:18:35
tags:
  - git
  - windows
  - socks
  - socks5
categories:
  - Windows
---
在win下没有找到类似tsocks的代理软件，又不想只为了一个git开vpn，可以用简单的一行git config开启socks5代理

	$ git config --global http.proxy 'socks5://127.0.0.1:1080'

So easy!