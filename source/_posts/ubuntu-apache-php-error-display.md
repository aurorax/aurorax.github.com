title: 开启ubuntu下apache+php的错误提示
tags:
  - apache
  - display
  - error
  - php
  - ubuntu
  - 开启
  - 错误提示
id: 586
comment: false
categories:
  - Ubuntu
date: 2013-10-25 20:25:13
---

ubuntu安装apache+php以后默认是没有错误提示的，需要手动开启。

1.修改php.ini
一般情况下在/etc/php5/apache2下
搜索display_errors改为

	display_errors = On

搜索error_reporting改为

	error_reporting = E_ALL | E_STRICT

2.修改httpd.conf
一般情况下在/etc/apache2目录下，是一个空白文件
添加以下两行：

	php_flag display_errors on
	php_value error_reporting 2039

3.重启Apache
命令行输入

	$ sudo /etc/init.d/apache2 restart