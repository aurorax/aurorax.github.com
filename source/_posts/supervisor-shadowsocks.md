title: centos使用supervisor管理shadowsocks
tags:
  - centos
  - shadowsocks
  - supervisor
id: 763
categories:
  - CentOS
  - Web
date: 2014-07-18 20:48:43
---

原先用goagent翻墙，可是太不稳定，看到linode也不算很贵，就买了最便宜的翻墙用。
shadowsocks的安装在github上写的很清楚了：
[https://github.com/clowwindy/shadowsocks](https://github.com/clowwindy/shadowsocks)
按照README.md配置好，运行

	$ ssserver -c /etc/shadowsocks.json
	
就可以连接了。
但是shadowsocks没有守护进程，关掉终端就会停止。
可以用nohup命令后台运行，但是不太稳定并且不易控制。
于是官方推荐用supervisor：
[https://github.com/clowwindy/shadowsocks/wiki/Configure-Shadowsocks-with-Supervisor](https://github.com/clowwindy/shadowsocks/wiki/Configure-Shadowsocks-with-Supervisor)
ubuntu/debian已经讲的很清楚了，说一下centos。

	$ yum install python-setuptools
	$ easy_install supervisor
	
然后创建配置文件

	$ echo_supervisord_conf > /etc/supervisord.conf
	
修改之

	$ vim /etc/supervisord.conf
	
在文件末尾添加

	[program:ssserver]
	command = ssserver -c /etc/shadowsocks.json
	autostart=true
	autorestart=true
	startsecs=3
	
配置文件的具体释义在这里
[http://supervisord.org/configuration.html](http://supervisord.org/configuration.html)
然后运行命令

	supervisord
	
最后设置开机启动

	$ vim /etc/rc.local
	
在末尾添加

	supervisord
	
保存，退出。
如果是centos7还需要为rc.local添加执行权限

	$ chmod +x /etc/rc.local
	
就全部完成了。
supervisor控制命令

	$ supervisorctl start ssserver     //开始ssserver
	$ supervisorctl stop ssserver      //终止ssserver
	$ supervisorctl restart ssserver   //重启ssserver</pre>