title: mac osx使用homebrew安装tsocks
date: 2015-06-12 20:07:43
tags:
	- mac
	- os
	- x
	- homebrew
	- brew
	- install
	- tsocks
id: 884
categories:
	- Mac
---

tsocks是一款在命令行下为其他软件应用代理的软件。

在mac下使用homebrew安装时会出现找不到formula的问题，homebrew的github上有这个问题的解决方法：
[https://github.com/Homebrew/homebrew/issues/11870](https://github.com/Homebrew/homebrew/issues/11870)

作者给出了formula代码

	require 'formula'

	class Tsocks < Formula
	  # The original is http://tsocks.sourceforge.net/
	  # This GitHub repo is a maintained fork with OSX support
	  homepage 'http://github.com/pc/tsocks'
	  head 'https://github.com/pc/tsocks.git'

	  depends_on 'autoconf' => :build if MacOS.xcode_version.to_f >= 4.3
	
	  def install
	    system "autoconf", "-v"
	    system "./configure", "--prefix=#{prefix}", "--disable-debug", "--disable-dependency-tracking", "--with-conf=#{config_file}"

	    inreplace("tsocks") { |bin| bin.change_make_var! "LIBDIR", lib }
	
	    system "make"
	    system "make install"

	    etc.install "tsocks.conf.simple.example" => "tsocks.conf" unless config_file.exist?
	  end
	
	  def test
	    puts 'Your current public ip is:'
	    ohai `curl -sS ifconfig.me 2>&1`.chomp
	    puts "If your correctly configured #{config_file}, this should show the ip you have trough the proxy"
	    puts 'Your ip through the proxy is:'
	    ohai `tsocks curl -sS ifconfig.me 2>&1`.chomp
	  end
	
	  def config_file
	    etc / 'tsocks.conf'
	  end
	end

然后

	$ vi /usr/local/Library/Formula/tsocks.rb

复制以上formula代码至此，然后命令行下

	$ brew install --HEAD tsocks
	
安装成功后

	$ vi /usr/local/etc/tsocks.conf
	
添加代码

	server = 127.0.0.1 ＃代理地址
	server_type = 5    ＃5即socks代理
	server_port = 8080 ＃代理端口

然后即可在命令行对任意软件应用代理

	$ tsocks wget https://google.com