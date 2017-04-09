title: 关于Godaddy主机空间主域名绑定子目录的方法
tags:
  - godaddy
  - 主机
  - 子目录
id: 28
categories:
  - Code
date: 2011-09-13 18:06:35
---

我买的是godaddyd deluxe+ssl，小菜鸟一个，不懂啊，就拿了个有用的域名绑上了，后面的事大家都知道了。
为了防止更菜的小菜鸟犯错误，这里说一下后果，用需要使用的主域名绑定空间，该域名不能绑定子目录，并且程序一旦出错就可能跳回根目录。
这里给大家一个利用.htacces重定向绑定子目录的方法，根目录下建立.htaccess（在win系统下是不可以的，可以建立a.htaccess上传以后改名），写入：
RewriteEngine on
RewriteCond %{REQUEST_FILENAME} !-f [OR]
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{HTTP_HOST} ^(.*.)?yourdomain.com$
RewriteCond %{REQUEST_URI} !^/yourdirectory/
RewriteRule ^(.*)$ /yourdirectory/$1
以上内容中yourdomain.com改为你自己的域名，即不能绑定子目录的主域名，yourdirectory改为子目录文件夹名，上传根目录即可。