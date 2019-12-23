---
layout: post
title: "有具体的需求，如何查找apt软件的名称？"
description: "Pi4 apt软件查找、安装、卸载的专题"
tag: pi4 raspbian
---   


## 需求
* 我想找个raspbian下的音乐播放器？用百度？
* 我想找个冷门的工具？百度无解，怎么办？
基于多个我想……，我在开发中发现了以下本地查询包名称的方案。



## 查询包名称的命令

```
sudo apt-cache search "xxx"

#比如我想找个音频播放器
sudo apt-cache search "audio player" 
得到关键词qmmp


sudo apt-cache search "foobar" 
得到关键信息lxmusic


#终端返回的信息量太大，怎么办？
cd ~
sudo apt-cache search "edit" >> 1.txt
然后查看1.txt文件

#显示更多用法：
sudo apt-cache --help


```

## 安装软件和卸载软件
```
#安装
sudo apt-get install qmmp -y

#卸载
sudo apt-get autoremove qmmp

#帮助
sudo apt-get --help

```


