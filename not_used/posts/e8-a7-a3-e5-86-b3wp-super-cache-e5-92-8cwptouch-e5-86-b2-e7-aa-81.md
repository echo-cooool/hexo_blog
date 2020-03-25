---
title: 解决WP Super Cache和WPtouch冲突
tags:
  - wordpress
url: 156.html
id: 156
categories:
  - Wordpress
date: 2018-04-14 14:58:26
---

首先进入WP Super Cache设置中；点击settings
================================

![](https://blog.csdn.net/qq_21438599/article/details/52917106)

然后修改以下4各地方；
===========

1.进入高级选中（Mobile device support. (External plugin or theme required. See the [FAQ](http://wordpress.org/plugins/wp-super-cache/faq/) for further details.)）点击更新（找不到向下翻） ![](https://blog.csdn.net/qq_21438599/article/details/52917106) 2.同样在高级设置中继续向下翻（已拒绝的用户代理(User Agent)）将下面这些复制进去点击更新

iPhone
iPod
Android
BB10
BlackBerry
webOS
IEMobile/7.0
IEMobile/9.0
IEMobile/10.0
MSIE 10.0
iPad
PlayBook
Xoom
P160U
SCH-I800
Nexus 7
Touch

3.在插件兼容选项中启用WPtouch ![](https://blog.csdn.net/qq_21438599/article/details/52917106) 4.最后在内容选项卡中删除已有缓存 ![](https://blog.csdn.net/qq_21438599/article/details/52917106)