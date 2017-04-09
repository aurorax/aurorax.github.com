title: “简明Python教程”的翻页插件
tags:
  - greasemonkey
  - javascript
  - python
  - tampermonkey
  - 简明Python教程
id: 513
categories:
  - Code
date: 2013-08-06 11:09:15
---

最近学习python，在看“[简明Python教程](http://woodpecker.org.cn/abyteofpython_cn/chinese/)”，其中翻页很麻烦，要用鼠标点下一页，于是就写了一个小插件，需要greasemonkey或者类似插件（在chrome使用的是tampermonkey），安装之后就可以按左右键翻页了。

	// ==UserScript==
	// @name       4PythonLearning
	// @namespace  http://woodpecker.org.cn/abyteofpython_cn/chinese/
	// @version    1.0.1
	// @description  designed for http://woodpecker.org.cn/abyteofpython_cn/chinese/ for page turning.
	// @match      http://woodpecker.org.cn/abyteofpython_cn/chinese/*.html
	// @copyright  2013+, aurorax
	// ==/UserScript==
	
	var as = document.getElementsByTagName("a");
	var last, next;
	for(i in as){
	    if(as[i].innerHTML == "上一页"){
        	last = as[i];	
    	}else if(as[i].innerHTML == "下一页"){
        	next = as[i];
    	}
	}
	//window.alert(last.innerHTML);
	document.onkeydown=jumpPage;
	
	function jumpPage() {
    	if (event.keyCode==37){//left button, last page
			last.click();
    	}
    	if (event.keyCode==39){//right button, next page
        	next.click();
    	}
	}
&nbsp;