title: 更换域名
id: 573
categories:
  - Web
date: 2013-10-05 23:22:45
tags:
---

[aurorax.org](http://aurorax.org/)终于掉下来了，可以抛弃.cn了。
抛弃.cn的原因太多了，多到我都不屑于写出来。
修改了.htaccess文件把所有的页面都跳转到新域名。
贴出来，适用于wordpress网站。

	# BEGIN WordPress
	<IfModule mod_rewrite.c>;
	RewriteEngine On
	RewriteCond %{HTTP_HOST} ^aurorax.cn [OR]
	RewriteCond %{HTTP_HOST} ^www.aurorax.cn [NC] 
	RewriteRule ^(.*)$ http://aurorax.org/$1 [L,R=301] 
	RewriteBase /
	RewriteRule ^index.php$ - [L]
	RewriteCond %{REQUEST_FILENAME} !-f
	RewriteCond %{REQUEST_FILENAME} !-d
	RewriteRule . /index.php [L]
	</IfModule>
	
	# END WordPress
	RewriteCond %{HTTP_HOST} ^www\.aurorax\.org$
	RewriteRule ^/?$ "http\:\/\/aurorax\.org\/" [R=301,L]