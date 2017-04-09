title: 'php:PHP_SELF,SCRIPT_NAME,REQUEST_URI'
tags:
  - php
  - PHP_SELF
  - REQUEST_URI
  - SCRIPT_NAME
id: 361
categories:
  - Code
date: 2012-12-31 09:03:13
---

最近用到，整理出来。

$_SERVER['PHP_SELF']

http://www.yoursite.com/example/ --- /example/index.php
http://www.yoursite.com/example/index.php --- /example/index.php
http://www.yoursite.com/example/index.php?a=test --- /example/index.php
http://www.yoursite.com/example/index.php/dir/test --- /dir/test
当使用$_SERVER['PHP_SELF']的时候，无论访问的URL地址是否有index.php，它都会自动的返回index.php。
但是如果在文件名后面再加斜线的话，就会把后面所有的内容都返回在$_SERVER['PHP_SELF']。

$_SERVER['REQUEST_URI']

http://www.yoursite.com/example/ --- /
http://www.yoursite.com/example/index.php --- /example/index.php
http://www.yoursite.com/example/index.php?a=test --- /example/index.php?a=test
http://www.yoursite.com/example/index.php/dir/test --- /example/index.php/dir/test
当使用$_SERVER['REQUEST_URI']的时候，返回的是我们在URL里写的精确的地址，如果URL只写到"/"，就返回 "/"

$_SERVER['SCRIPT_NAME']

http://www.yoursite.com/example/ --- /example/index.php
http://www.yoursite.com/example/index.php --- /example/index.php
http://www.yoursite.com/example/index.php --- /example/index.php
http://www.yoursite.com/example/index.php/dir/test --- /example/index.php
所有的返回中都是当前的文件名/example/index.php