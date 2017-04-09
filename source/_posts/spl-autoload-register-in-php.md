title: 'php:spl_autoload_register()'
tags:
  - php
  - spl_autoload_register
id: 282
categories:
  - Code
date: 2012-09-24 00:38:41
---

学习yii框架的时候看到这个函数，查了一下资料，整理如下。
作用是注册自定义__autoload()函数。
1\. bool spl_autoload_register('function')
参数为自定义自动加载函数名，返回布尔值。
例：

	<?php

	function autoload($class){
		require '$class.php';
	}

	spl_autoload_register('autoload');

2\. bool spl_autoload_register(array('class','static_function'))

参数为数组，数组中第一个值为类名，第二个值为方法名，且必须为静态方法。

例：

	<?php

	class A
	{
		public static function autoload($class){
			require '$class.php';
		}
	}

	spl_autoload_register(array('A','autoload'));
	