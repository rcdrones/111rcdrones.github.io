---
layout: post
title: "树莓派1.6寸CPU Mini液晶背光软件控制方法"
description: ""

tag: 树莓派外设
---


## 前言
  cpu mini液晶从诞生到现在经历了多次升级，目前最新版本，可以用软件来控制背光的开关。下面我们来讲讲如何操作的。
![img](/images/posts/cpuinfo/show.gif)


### 硬件修改
![img](/images/posts/cpuinfo/hw.jpg)
<p></p>
![img](/images/posts/cpuinfo/hw2.jpg)

### 软件
编写程序`nano bl.c`

    #include <wiringPi.h>
    int main (void)
    {
        wiringPiSetup () ;
        pinMode (7, OUTPUT) ;
        for (;;)
        {
            digitalWrite (7, HIGH) ; delay (500) ;
            digitalWrite (7,  LOW) ; delay (500) ;
        }
        return 0 ;
    }
    

编译成可执行文件：

	gcc -Wall -o bl bl.c -lwiringPi
	sudo ./bl

> 特别注意：
> 用软件来控制GPIO7的时候， 一定要先把背光开关打到OFF档位，然后再短路背面的焊盘。否则容易引起 GPIO7 电平冲突。原理如下：当GPIO7输出为低电平时LED背光点亮，这里没问题。 当GPIO7输出高电平（3.3V）时，如果外部把背光开关打到ON档位。 3.3V和GND就会短路，重则烧毁树莓派。所以务必用软件控制背光的同学。一定吧开关打到OFF档位上。



