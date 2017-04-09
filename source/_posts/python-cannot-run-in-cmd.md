title: python不能在cmd下运行
id: 536
categories:
  - Code
date: 2013-08-27 21:49:32
tags:
---

困扰我挺长时间一个问题，今天从stackoverflow查到，原来是环境变量的问题，搬运一下。

[http://stackoverflow.com/questions/6318156/adding-python-path-on-windows-7](http://stackoverflow.com/questions/6318156/adding-python-path-on-windows-7)
Watch out for these possible mistakes:
1.Kill and reopen your shell window: Once you make a change to the ENVIRONMENTAL Variables, you have to restart the window you are testing it on.
2.NO SPACES when setting the Variables. Make sure that you are adding the ;C:\Python27 WITHOUT any spaces. (It is common to try C:\SomeOther; C:\Python27 That space (_) after the semicolon is not okay.)
3.USE A BACKWARD SLASH when spelling out your full path. You will see forward slashes when you try echo $PATH but only forward slashes have worked for me.
4.DO NOT ADD a final backslash. Only C:\Python27 NOT C:\Python27\

关于环境变量的设置，注意一下几点（翻译顺序有变动，感觉这样操作起来更合理）：
1.添加环境变量时不要带空格。例如: C:\SomeOther; C:\Python27 分号后面不能有空格。正确形式:C:\SomeOther;C:\Python27
2.路径中使用反斜线“\”。
3.路径最后不要加反斜线。使用 C:\Python27 而不是 C:\Python27\
4.设置完毕后重启cmd。