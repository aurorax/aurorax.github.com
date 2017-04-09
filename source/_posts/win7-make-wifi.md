title: win7无线网络热点的设置
tags:
  - wifi
  - win7
id: 228
categories:
  - Code
date: 2012-08-30 17:23:10
---

假期出去玩，酒店没有wifi，就在网上搜了下用朋友的笔记本做了一个热点。
测试速度一般，但总比没有强，记下来以备后用。
其实就两行命令，但还是写清楚吧，省得解释。
前提是你的笔记本有无线网卡...
打开“开始-程序-附件”，在“命令提示符”上单击右键，选择“以管理员身份运行”。
输入netsh wlan set hostednetwork mode=allow ssid=你想设置的wifi名称 key=你想设置的wifi密码
名称必须为英文，密码必须大于8位，回车即可。
再输入netsh wlan start hostednetwork
回车，然后进入“网络和共享中心-更改适配器设置”。
此时应该会出现一个网卡名为“Microsoft Virtual WiFi Miniport Adapter”的无线连接。
右键单击正在使用的链接（就是可以上网的链接），选择“属性”，选择“共享”选项卡，勾选“允许其他...”，并选择新出现的无线连接，确定就可以了。
每次开机以后需要运行一次netsh wlan start hostednetwork才可以使用wifi。
为了简便可以把这两句话分两行写在一个记事本里，然后把记事本后缀.txt改成.bat，每次需要使用的时候单击右键“以管理员身份运行”就可以了。