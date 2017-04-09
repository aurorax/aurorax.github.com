title: 遥控车的舵机与电调控制
tags:
  - arduino
  - 兴耀华
  - 小车
  - 电调
  - 舵机
  - 遥控车
id: 401
categories:
  - Code
date: 2013-04-10 13:02:55
---

挺长一段时间以前就看到某宝上有四轮驱动底盘，价格也不贵，最近一段时间闲下来，买了一个。
做工什么的还算说得过去，物有所值吧。
遥控车的控制比四轴是要简单多了，除了控制芯片就没了。
当然这是在最简单的完成基本控制的前提下，如果想要智能起来，还是需要配合其他传感器和芯片，复杂程度就提高了。
上代码吧。

	#include "Servo.h"
	
	float c1, c2, c3, c4;
	Servo motor, wheel;
	int flag = 1, delays = 10;
	
	void setup(){
	  motor.attach(9);
	  turn.attach(10);
	  pinMode(A0, INPUT);
	  pinMode(A1, INPUT);
	  pinMode(A2, INPUT);
	  pinMode(A3, INPUT);
	}
	
	void loop(){
	  c1 = pulseIn(A0, HIGH);
	  c2 = pulseIn(A1, HIGH);
	  c3 = pulseIn(A2, HIGH);
	  c4 = pulseIn(A3, HIGH);
	  if(delays <= 0){
	    if(c2 > 1800){
	      flag=1;
	    }else if(c2 < 1200){
	      flag=0;
	    }
	  }
	  delays -= 1;
	    if(flag == 0){
	      c3 = map(c3,1100,1900,90,130);
	    }else if(flag == 1){
	      c3 = map(c3,1100,1900,90,50);
	    }
	    c1 = map(c1,1080,1850,125,65);
	    motor.write(c3);
	    turn.write(c1);
	}
	
解释一下，遥控车的控制其实是最简单的了，只需要两通道。一般遥控车都是用枪控，手头没有枪控，再买一个就不大划算，于是就上板控。
如果把上述代码直接写入arduino芯片，油门就是油门，俯仰上推是挂前进挡，下推是后退挡，横滚是转向。
买来的底盘带舵机带电调，舵机不用说肯定是pwm，电调不太清楚，有刷电调貌似都是pwm控制，前段时间玩的4轴无刷电调是直接用电压控制。
pwm控制直接利用arduino的Servo库，很简单，已经包含在官方包里，不需要include直接调用就可以。
舵机接上5v电压地线信号线，调试到横滚行程恰好是前轮转向的最大行程就好。然后就是电机和电调。手上的这个电调对占空比比较敏感，并且没有说明书，甚至根本查不到这个电调的资料= =#，于是就写了一个利用遥控器调节占空比的程序，并且用串口输出，测得利用Servo.write输出大概90左右就可以通过电调自检，并使电机处于停止状态。程序简单给一下吧，很简单，读取遥控pwm然后map一下输出就好了。

	Servo motor;
	c3 = pulseIn(A2, HIGH);
	c3 = map(c3,1100,1900,130,50);
	motor.write(c3);

顺便给出电调型号：兴耀华 ZD ESC-150A
整个电调上就只有这个几个字母，厂名是从卖家那里得到的，从来没听说过...
到这里遥控车的控制部分基本就完成了，后续智能部分如果做出来了会继续更新。