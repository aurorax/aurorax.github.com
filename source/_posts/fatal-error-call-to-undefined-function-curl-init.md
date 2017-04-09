title: 'Fatal error: Call to undefined function curl_init()'
tags:
  - Call to undefined function curl_init()
  - curl
  - php
  - 'PHP Startup:Unable to load dynamic library'
  - 因为应用程序的并行配置不正确
  - 应用程序无法启动
  - 无法加载
  - 无法启动
id: 471
categories:
  - Code
date: 2013-06-12 11:34:30
---

这个问题困扰了我两天。出现这个错误以后我就开始四处搜寻解决办法，下面就把我搜索到关于curl问题可能的解决方案写出来。
一般win系统下加载curl，就是在php.ini中去掉“;extension=php_curl.dll”之前的分号，不过要注意加载的是哪个php.ini，可以通过phpinfo()得到具体的加载情况，其中“Loaded Configuration File”项就是当前加载的php.ini路径，需要更改这个路径下的php.ini中的分号才可以正常加载。更改之后刷新一遍phpinfo()页面，如果加载成功，是可以在刷新后的页面里找到curl项的。网页搜索curl即可，如果搜索不到结果就是没有加载。
如果经过上述过程还是没有正常加载，那么可能就是你的环境变量出了问题。请看这里框框里的文字
[http://nz.php.net/manual/en/curl.installation.php](http://nz.php.net/manual/en/curl.installation.php)
windows下php_curl.dll的加载是需要libeay32.dll和ssleay32.dll作为支持的，简单的办法是把php目录下的这两个dll复制到系统目录system32文件夹下，或者把php文件夹路径加入到当前系统变量中，如何添加自行谷歌。
如果经过上述过程还是在phpinfo()中找不到curl，那么恭喜你，你的情况应该大致和我相同，不过好的方面是你不需要被困扰两天了。
我是在64位win7下使用wampserver架构环境的，php版本是5.3.13。而此版本的php_curl.dll是不兼容64位win系统的，所以需要替换文件，找了很久才在这个博客里找到和合适的dll文件。
[http://www.macnie.com/posts/view/28](http://www.macnie.com/posts/view/28)
要说明的是这个curl是x64windows下可用，如果你是别的版本可能还需要自己去找。
如果在x64windows下替换过后还是不能正常加载，那就只能另寻他路了，重新下载最新版本的php并重新构架环境应该是最好的选择。