---
layout: post
title: "树莓派CPU Mini液晶使用教学"
description: ""

tag: 树莓派外设
---



## 教程：

樹莓派上觀察CPU及RAM使用率的剩餘容量，是比較有趣的事情。同時如果樹莓派做伺服器，也可以看到linux RAM的使用變化。

* 硬體篇
　Pi的插入方式： 
　![img](/images/posts/cpuinfo/1.jpg)

* 軟體篇
 1. 先安裝wiring pi.

```
cd ~
git clone git://git.drogon.net/wiringPi
cd wiringPi
./build
```

2. 建立工作目錄
```
cd ~
mkdir cpu_show
```
3. 用sftp 的方法下載源代碼到/home/pi/cpu_show 下
4. 編譯源代碼
```
cd ~/cpu_show

cc -o cpushow pcd8544_rpi.c PCD8544.c  -L/usr/local/lib -lwiringPi

//最後執行看效果
sudo ./cpushow
```

### 對比度修改知識
```
//由於每個液晶的明暗對比度有差異，如果大家發現
//顯示的內容太黑了。或者顯示的內容太淡了。
//需要修改pcd8544_rpi.c 這個源代碼的對比度變量，然後在重新編譯，並運行看效果變化！
nano pcd8544_rpi.c
// lcd contrast
//may be need modify to fit your screen!  normal: 30- 90 ,default is:45 !!!maybe modify this value!
int contrast = 45;
//修改這裡，默認是45，太黑了，就減少一點，5是不錯的步進指數。
//太淡了，增加5
//改完後重新編譯在運行
cc -o cpushow pcd8544_rpi.c PCD8544.c  -L/usr/local/lib -lwiringPi
sudo ./cpushow
```


### 如果需要開機就自動運行cpushow
```
sudo nano /etc/rc.local
在最後一行exi​​t 0 以上加入如下內容：
sudo /home/pi/cpu_show/cpushow
此外玩家可以根據修改.c代碼，進行顯示其他內容。
液晶的分辨率是84*48 個點，編程後，想顯示什麼就顯示什麼。
```