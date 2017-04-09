title: 使用谷歌加载jQuery的原因
tags:
  - google
  - jquery
id: 153
categories:
  - Code
date: 2012-04-15 14:55:08
---

[3 reasons why you should let Google host jQuery for you](http://www.ajaxlines.com/ajax/stuff/article/_reasons_why_you_should_let_google_host_jquery_for_you.php) 翻译原文：（实在懒得翻译了）[为什么推荐使用谷歌加载jquery库文件](http://www.skygq.com/2011/03/10/%e4%b8%ba%e4%bb%80%e4%b9%88%e6%8e%a8%e8%8d%90%e4%bd%bf%e7%94%a8%e8%b0%b7%e6%ad%8c%e5%8a%a0%e8%bd%bdjquery%e5%ba%93%e6%96%87%e4%bb%b6/) 1.减少等待时间 CDN-Content Delivery Network（内容发布网络）的缩写，通过各种各样的服务途径把你的一些静态内容分散开来，当用户的浏览器提交这些文件的链接请求，他们便会自动下载网络上最近的可用的文件。 因为这个原因：任何使用你服务的用户从谷歌下载JQuery库都将获得比从你自己的服务器上下载更快的速度。其实有很多的CDN服务可与谷歌的相比拟，但是他们很难超越谷歌的免费服务的优势，这个益处足以决定问题，但这仅仅是一部分。 2.增加网页的同时载入速度 为了避免服务的过载，浏览器限制了同时连接的数目，依据不同的浏览器，这个限制可能是每个机房仅仅两个之少。 使用谷歌的AJAX内容服务网络来响应你的网站，使你本地服务器上更多服务可以同时进行，这和用户同时用6个浏览器浏览的效果没多大诧异，但是（那些不这么做的人）任然是运行一个浏览器，仅仅允许同时链接两个（链接数目到你的服务器上），这里的区别显而易见。 3.更好的缓存 利用谷歌AJAX图书馆内容发布服务的最大好处是你的用户根本不需要下载jQuery.不论你的缓存多么强大，如果你用自己的服务器提供jQuery，那么你的用户至少要下载一次它，某个用户很有可能在他们浏览器的缓存区里下载了许多完全相同的jQuery.min.js的拷贝版本，但是当他们第一次访问你的网站的时候，这些拷贝版本会被忽略。 另一方面，当浏览器检测到同样版本的指向谷歌的链接，它就会知道这是下载同一个文件，不仅是谷歌的服务器会返回一个304（不需要修改文件的指令，即服务器上的文件未改动过）来回复一个重复的请求，而且会命令浏览器的缓存该文件长达一年的时间。 这意味着即使一些人访问了数百的使用谷歌服务的jQuery网站,他们只需要下载一次就够了。 一旦谷歌服务器不能访问（这个可能性不大，更多的可能是被墙），译文给出了解决的办法

	<SCRIPT type=text/javascript src="http://ajax.googleapis.com/ajax/libs/jquery/1.4/jquery.min.js"></SCRIPT>
	<script>!window.jQuery && document.write('<SCRIPT src="jquery-1.4.3.min.js"></SCRIPT>');</script>