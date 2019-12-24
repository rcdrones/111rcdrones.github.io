---
layout: post
title: "树莓派启动后，自动激活numlock "
description: ""

tag: Pi4-入门 
---   



Raspbian反人类的设计，默认是numlock关闭的。 导致输入密码容易出错，解决方案如下：





### 安装numlockx: 

`sudo apt-get install numlockx`





### 编辑如下文件：

`sudo nano /usr/share/lightdm/lightdm.conf.d/01_debian.conf`



在文件的最后添加一个新行：

`greeter-setup-script=/usr/bin/numlockx on`



保存后，重启pi4。numlock应该会自动开启了。