title: php取整函数
tags:
  - php
  - 取整
id: 125
categories:
  - Code
date: 2012-03-07 13:29:12
---

今天写程序需要用到取整，查了一下一共有三种取整函数。

&nbsp;

1.舍去法取整 floor()

语法格式 float floor(float value)

舍弃value的小数部分，返回value的整数部分，返回值类型依然是float。

echo floor(5.4);

5

echo floor(9.999)

9

&nbsp;

2.进一法取整 ceil()

语法格式 float ceil(float value)

value如果有小数部分，则返回value的整数部分+1。返回值类型依然然是float。

echo ceil(5.4);

6

echo ceil(9.999);

10

&nbsp;

3.四舍五入取整 round()

语法格式 float round(float val [, int precision])

四舍五入取整，第二个形参表示取整位数。返回值类型为float。

echo round(5.4345); 

3

echo round(5.5345);

4

echo round(5.6345);

4

echo round(5.6345, 0); 

4

echo round(5.4345, 2);

5.43

echo round(543456, -3);

543000