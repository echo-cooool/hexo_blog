---
title: proxmox搭建记录
url: 15044.html
id: 15044
categories:
  - Computer
date: 2018-11-09 22:26:28
tags:
---

[Proxmox VE](http://pve.proxmox.com/wiki/Main_Page)(Proxmox Virtual Environment) 是一款完全开源虚拟化管理平台，可以管理QEMU/KVM虚拟机和LXC容器。事实上它只是一个前端管理界面，虚拟化技术由KVM和LXC提供。 ![](http://blog.echo.cool/wp-content/uploads/2018/11/1-1024x549.jpg) ![](http://blog.echo.cool/wp-content/uploads/2018/11/2-1024x549.jpg)

### 安装Proxmox VE

首先到官网下载Promox VE的镜像文件。 下载地址：[https://www.proxmox.com/en/downloads/item/proxmox-ve-4-4-iso-installer](https://www.proxmox.com/en/downloads/item/proxmox-ve-4-4-iso-installer) 下载完成后，使用dd命令或者USBWriter将镜像内容写入U盘,制作引导盘。 `dd if=proxmox-ve_4.4-eb2d6f1e-2.iso of=/dev/sdc bs=4m` 开始安装前，先用网线连接x86主机和路由器（目的是为了我的笔记本可以访问Proxmox的web界面），然后插入U盘进行引导，出现如下安装界面 \[caption id="attachment_15049" align="alignnone" width="642"\]![](http://blog.echo.cool/wp-content/uploads/2018/11/proxmox搭建记录.png) \[/caption\]

### 配置Proxmox VE

启动Proxmox VE后会提示访问网址，使用笔记本访问 [https://192.168.1.100:8006](https://192.168.1.100:8006/) ,并输入 root/刚刚设置的密码 进行登录。

挂载硬盘
----

在shell中输入mkdir /mnt/sdb创建sdb[文件夹](https://www.smzdm.com/fenlei/wenjianjia/)用来给磁盘挂载 输入fdisk /dev/sdb管理这个硬盘，给它分区 输入n新建分区 [![基于ProXmoX VE的虚拟化家庭服务器（篇一）—ProXmoX VE 安装及基础配置](https://am.zdmimg.com/201809/17/5b9f4978be99b1781.png_e600.jpg)](https://post.smzdm.com/p/a3k2r5r/pic_14/) 输入p建立主分区， [![基于ProXmoX VE的虚拟化家庭服务器（篇一）—ProXmoX VE 安装及基础配置](https://am.zdmimg.com/201809/17/5b9f49791b0d89311.png_e600.jpg)](https://post.smzdm.com/p/a3k2r5r/pic_15/) 输入1创建一个分区， [![基于ProXmoX VE的虚拟化家庭服务器（篇一）—ProXmoX VE 安装及基础配置](https://am.zdmimg.com/201809/17/5b9f49790c5c72082.png_e600.jpg)](https://post.smzdm.com/p/a3k2r5r/pic_16/) 这里是让输入这个分区的扇区起始位置，我们选择默认，直接回车 [![基于ProXmoX VE的虚拟化家庭服务器（篇一）—ProXmoX VE 安装及基础配置](https://am.zdmimg.com/201809/17/5b9f497931d597756.png_e600.jpg)](https://post.smzdm.com/p/a3k2r5r/pic_17/) 分区的扇区结束位置，默认，直接回车，到此就分区完成了，我们输入p查看一下 \[caption id="attachment_15050" align="alignnone" width="600"\]![基于ProXmoX VE的虚拟化家庭服务器（篇一）—ProXmoX VE 安装及基础配置](http://blog.echo.cool/wp-content/uploads/2018/11/proxmox搭建记录.jpg) 基于ProXmoX VE的虚拟化家庭服务器（篇一）—ProXmoX VE 安装及基础配置\[/caption\] 分区已经完成，目录为/dev/sdb1 输入w，保存并退出fdisk工具 输入mkfs -t ext4/dev/sdb1格式化一下 输入 mount/dev/sdb1 /mnt/sdb进行挂载