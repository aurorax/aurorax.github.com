title: arduino控制mpu6050进行姿态角测量及卡尔曼滤波
tags:
  - arduino
  - filter
  - kalmen
  - mpu6050
  - 卡尔曼
  - 姿态
  - 姿态角
  - 数据融合
  - 滤波
id: 372
categories:
  - Code
date: 2013-01-31 09:10:48
---

关于四轴飞行器的飞控程序，最近有了点阶段性成果，写出来给大家作参考。
参考了太多资料了，地址都没记下来，没法贴出来。如果你发现有你的东西，请联系我。
刚开始学习的时候买的是Arduino UNO，很大但是接线方便。后来焊板子用的就是nano了。
首先说一下mpu6050的加速度与角速度的数据融合。但是得到的波形很不理想，于是就转向DMP了。
开始...
直接上程序...

	#include "Wire.h"
	#include "I2Cdev.h"
	#include "MPU6050.h"
	
	MPU6050 accelgyro;
	
	unsigned long now, lastTime = 0;
	float dt;                                   //微分时间
	
	int16_t ax, ay, az, gx, gy, gz;             //加速度计陀螺仪原始数据
	float aax=0, aay=0, agx=0, agy=0, agz=0;    //角度变量
	long axo = 0, ayo = 0, azo = 0;             //加速度计偏移量
	long gxo = 0, gyo = 0, gzo = 0;             //陀螺仪偏移量
	
	float pi = 3.1415926;
	float AcceRatio = 16384.0;                  //加速度计比例系数
	float GyroRatio = 131.0;                    //陀螺仪比例系数
	
	uint8_t n_sample = 8;                       //加速度计滤波算法采样个数
	float aaxs[8] = {0}, aays[8] = {0};         //x,y轴采样队列
	long aax_sum, aay_sum;                      //x,y轴采样和
	
	float a_x[10]={0}, a_y[10]={0} ,g_x[10]={0} ,g_y[10]={0}; //加速度计协方差计算队列
	float Px=1, Rx, Kx, Sx, Vx, Qx;             //x轴卡尔曼变量
	float Py=1, Ry, Ky, Sy, Vy, Qy;             //y轴卡尔曼变量
	
	void setup() {
	  Wire.begin();
	  Serial.begin(9600);
	
	  accelgyro.initialize();                 //初始化
	
	  unsigned short times = 200;             //采样次数
	  for(int i=0;i<times;i++){
	    accelgyro.getMotion6(&ax, &ay, &az, &gx, &gy, &gz); //读取六轴原始数值
	    axo += ax; ayo += ay; azo += az;      //采样和
	    gxo += gx; gyo += gy; gzo += gz;
	  }
	  axo /= times; ayo /= times; azo /= times; //计算加速度计偏移
	  gxo /= times; gyo /= times; gzo /= times; //计算陀螺仪偏移
	}
	
	void loop(){
	  unsigned long now = millis();             //当前时间(ms)
	  dt = (now - lastTime) / 1000.0;           //微分时间(s)
	  lastTime = now;                           //上一次采样时间(ms)
	
	  accelgyro.getMotion6(&ax, &ay, &az, &gx, &gy, &gz); //读取六轴原始数值
	
	  float accx = ax / AcceRatio;              //x轴加速度
	  float accy = ay / AcceRatio;              //y轴加速度
	  float accz = az / AcceRatio;              //z轴加速度
	
	  aax = atan(accy / accz) * (-180) / pi;    //x轴对于水平面的夹角
	  aay = atan(accx / accz) * 180 / pi;       //y轴对于水平面的夹角
	
	  aax_sum = 0;                              // 对于加速度计原始数据的滑动加权滤波算法
	  aay_sum = 0;
	  for(int i=1;i<n_sample;i++){
	    aaxs[i-1] = aaxs[i];
	    aax_sum += aaxs[i] * i;
	    aays[i-1] = aays[i];
	    aay_sum += aays[i] * i;
	  }
	  aaxs[n_sample-1] = aax;
	  aax_sum += aax * n_sample;
	  aax = (aax_sum / (11*n_sample/2.0)) * 9 / 7.0; //角度调幅至0-90°
	  aays[n_sample-1] = aay;                        //此处应用实验法取得合适的系数
	  aay_sum += aay * n_sample;                     //本例系数为9/7
	  aay = (aay_sum / (11*n_sample/2.0)) * 9 / 7.0;
	
	  float gyrox = - (gx-gxo) / GyroRatio * dt; //x轴角速度
	  float gyroy = - (gy-gyo) / GyroRatio * dt; //y轴角速度
	  agx += gyrox;                             //x轴角速度积分
	  agy += gyroy;                             //x轴角速度积分
	
	  /* kalmen start */
	  Sx = 0; Rx = 0;
	  Sy = 0; Ry = 0;
	  for(int i=1;i&lt;10;i++){                 //测量值平均值运算
	    a_x[i-1] = a_x[i];                      //即加速度平均值
	    Sx += a_x[i];
	    a_y[i-1] = a_y[i];
	    Sy += a_y[i];
	  }
	  a_x[9] = aax;
	  Sx += aax;
	  Sx /= 10;                                 //x轴加速度平均值
	  a_y[9] = aay;
	  Sy += aay;
	  Sy /= 10;                                 //y轴加速度平均值
	
	  for(int i=0;i&lt;10;i++){
	    Rx += sq(a_x[i] - Sx);
	    Ry += sq(a_y[i] - Sy);
	  }
	  Rx = Rx / 9;                              //得到方差
	  Ry = Ry / 9;                        
	
	  Px = Px + 0.0025;                         // 0.0025在下面有说明...
	  Kx = Px / (Px + Rx);                      //计算卡尔曼增益
	  agx = agx + Kx * (aax - agx);             //陀螺仪角度与加速度计速度叠加
	  Px = (1 - Kx) * Px;                       //更新p值
	
	  Py = Py + 0.0025;
	  Ky = Py / (Py + Ry);
	  agy = agy + Ky * (aay - agy); 
	  Py = (1 - Ky) * Py;
	
	  /* kalmen end */
	
	  Serial.print(agx);Serial.print(",");
	  Serial.print(agy);Serial.println();

解释一下程序。
采样200次取平均值计算加速度计和陀螺仪的偏差。
进入循环，用反正切求出加速度角度，滑动采样8次进行滑动加权滤波，乘以用实验法获得的系数，以调整角度到正确的值。
对角速度积分得到陀螺仪角度，进入卡尔曼滤波。
其实对于卡尔曼滤波公式我也没大看懂，公式是从别人那抄的，我稍稍修改了一下，看起来更像一个自适应的互补滤波。
对加速度角度建立一个滑动采样队列，采样数为10，求出队列方差，并适当缩小后（本例为缩小5倍），运算得到卡尔曼增益。
加速度角度与陀螺仪角度做差后，乘以卡尔曼增益叠加到陀螺仪角度上。更新P值。
*******
得到的波形并不是很理想，只是给大家提供一个思路。
由于后来改用mpu6050的dmp了，程序最后也没有仔细验证，如果测试有问题可以给我留言。
关于dmp的应用，后面再写吧。