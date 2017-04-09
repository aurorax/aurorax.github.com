title: dns.la动态域名脚本ddnsla
tags:
  - ddns
  - dns.la
  - raspberry pi
  - 免费
  - 动态域名
  - 绑定
id: 712
categories:
  - Code
  - Web
date: 2013-12-28 16:55:47
---

DDNS(Dynamic Domain Name System)动态域名系统，解决了非固定ip的域名解析问题，国内外很多网站提供这类服务，例如花生壳。
但是前一阵花生壳推出“新花生壳”之后，竟然停止了顶级域名的免费ns导入解析，如果需要使用花生壳ddns解析顶级域名，每年每个域名需要交40元。
不愿意交钱，并且免费级的解析记录更新时间一般很长，搜索了一下其他的ddns服务，发现花生壳竟然还算便宜的，于是决定自己解决问题。
由于域名在国外，使用的是dns.la的解析服务，查看了一下发现开放了api，于是着手用python写了一个小脚本。
源码：[https://github.com/aurorax/ddnsla](https://github.com/aurorax/ddnsla)
需要一个具有外网ip的网络接口，一个raspberry pi或是任何可以跑python脚本的东西。
注册一个dns.la帐号，开启账号的api，会得到一个apiid和api密钥。在域名服务商处修改域名的NS地址，使域名dns转移至dns.la，等待修改生效，然后添加一条需要解析的A记录。
下载ddns.py，用任何文档编辑器打开。

	tz = 'Asia/Shanghai'
	apiid = 'test'
	apipass = 'pass'
	domain = 'domain.com'
	host = '@'
	type = 'A'
	ttl = '300'
	loop = 5 #seconds

需要修改的就是前面的几个变量。tz是时区，apiid和apipass分别更改为dns.la帐号得到的apiid和api密钥，domain是添加到帐号中需要ddns服务的域名，host为域名前缀，ttl就是ttl，loop是检查的间隔时间。
需要注意的是，dns.la限制了api调用频率，每小时不超过300次，每天不超过3000次，超出会有惩罚。
详见api文档：[https://www.dns.la/api/doc/](https://www.dns.la/api/doc/)
脚本正常循环时不调用api，默认为每5s检查本机ip与域名ip是否相同，相同继续循环，不调用api，不同则修改域名ip，每次修改调用2次api。
所以如果ip更换十分频繁就要考虑将loop值增大，加长循环周期，降低调用频率。
其实算一下就可以得到，正常情况下的ip变更是不会超出api调用频率限制的，不需要调整loop。
还有获取本机和域名的ip地址使用的是ip.cn页面，正则提取其中显示的第一个ip，如果需要更换其他的ip地址检查页面可以更改getIP()中的一下变量。
修改完毕后，linux中可以后台运行：

	$ nohup python ddns.py &
	
查看进程：

	$ ps -ef | grep ddns

至此动态域名解析就完成了，暂时只支持单个域名的ddns，如果需要多个域名的ddns可以复制多个脚本，分别更改配置参数就好了。