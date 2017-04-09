title: wordpress关闭新用户注册邮件
tags:
  - wordpress
  - 关闭
  - 新用户
  - 注册
  - 邮件
id: 592
categories:
  - Code
date: 2013-10-27 21:16:49
---

wordpress升级了3.7，又开始发新用户注册邮件了。又搜索了一下如何关闭，贴出来。

打开wp-includes/pluggable.php文件，搜索

	@wp_mail(get_option('admin_email'), sprintf(__('[%s] New User Registration'), $blogname), $message);
	
注释本条语句，就不会自动发出新用户注册邮件了。