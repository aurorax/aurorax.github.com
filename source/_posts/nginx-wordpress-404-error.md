title: nginx环境下安装wordpress文章出现404无法访问
tags:
  - '404'
  - nginx
  - wordpress
  - 文章
  - 无法访问
id: 789
categories:
  - CentOS
  - Web
date: 2014-08-22 15:38:44
---

如果wordpress需要使用固定链接，则需要对服务器做rewrite设置。
apache只需要添加一个.htaccess文件即可，nginx需要对配置文件作出修改。
编辑nginx的配置文件

	$ sudo vim /etc/nginx/conf.d/default.conf
	
在“location /”中追加“try_files $uri $uri/ /index.php?$args;”

	location / {
    	index  index.php index.html index.htm;

    	# nginx configuration
    	try_files $uri $uri/ /index.php?$args;
	}

重启nginx服务即可

	$ sudo service nginx restart