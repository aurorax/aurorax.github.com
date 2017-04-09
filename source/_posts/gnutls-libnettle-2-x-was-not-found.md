title: 'GnuTLS: Libnettle 2.x was not found'
tags:
  - gnutls
  - nettle
  - not found
  - prefix
id: 882
categories:
  - CentOS
  - Code
date: 2015-05-24 18:39:51
---

在安装gnutls的时候如果遇到“Libnettle 2.x was not found”，一般有两个原因。

1.nettle未安装
这个比较简单，默认centos

	$ wget http://ftp.gnu.org/gnu/nettle/nettle-2.x.x.tar.gz
	$ tar zxf nettle-2.x.x.tar.gz && cd nettle-2.x.x
	$ ./configure && make && make install
	
其中2.x.x为所需的版本号，安装完毕即可继续安装gnutls。

2.环境变量
这个我花了一段时间才搞明白，一般出现在64位系统中，如果nettle没有安装在默认位置，而是“--prefix=/opt”，则须修改环境变量，以“--prefix=/opt”为例

	$ export LD_LIBRARY_PATH=/usr/lib/:/usr/lib64/:/opt/lib/:/opt/lib64/ NETTLE_CFLAGS="-I/opt/include/" NETTLE_LIBS="-L/opt/lib64/ -lnettle" HOGWEED_CFLAGS="-I/opt/include" HOGWEED_LIBS="-L/opt/lib64/ -lhogweed"
	
然后即可安装gnutls。