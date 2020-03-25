---
title: 变色龙侦测卡——ChameleonMini
url: 14840.html
id: 14840
categories:
  - 安全测试
date: 2018-07-28 16:38:08
tags:
---

软件使用：
=====

![](http://blog.echo.cool/wp-content/uploads/2018/07/1.软件结构总览-1024x730.png) ![](http://blog.echo.cool/wp-content/uploads/2018/07/2.配置成一张IC卡.png) ![](http://blog.echo.cool/wp-content/uploads/2018/07/3.使用侦测卡侦测秘钥.png) ![](http://blog.echo.cool/wp-content/uploads/2018/07/4.按钮功能的设置.png)

升级固件：
=====

![](http://blog.echo.cool/wp-content/uploads/2018/07/1.连接设备进入固件升级模式-1024x667.png) ![](http://blog.echo.cool/wp-content/uploads/2018/07/2.安装固件升级用驱动.png) ![](http://blog.echo.cool/wp-content/uploads/2018/07/3.点第二个.png) ![](http://blog.echo.cool/wp-content/uploads/2018/07/4.点第二个.png) ![](http://blog.echo.cool/wp-content/uploads/2018/07/5.下一步.png) ![](http://blog.echo.cool/wp-content/uploads/2018/07/6.点从磁盘安装，选择驱动安装-1024x427.png) ![](http://blog.echo.cool/wp-content/uploads/2018/07/7.安装成功.png) ![](http://blog.echo.cool/wp-content/uploads/2018/07/8.驱动安装成功.png) ![](http://blog.echo.cool/wp-content/uploads/2018/07/9.运行BOOT烧录程序进行烧录-1024x338.png)

常见问题：
=====

### 1.为什么上传了数据，读头却不识别，刷卡没反应？

a.各别读头瞬间验证两个以上的扇区，速度过快，变色龙反应不过来，会造成识别不到。 b.读头猝发读卡时间比较短，尝试按住红色按钮供电来刷卡。 c.原卡可能是含有特别指令的防复制IC卡，变色龙本身是可以穿防火墙的， 反UID，反CUID的系统都可以识别

### 2.为什么设置了侦测卡之后，刷卡回来，获取不到秘钥？

a.一般情况点【快速解】，如果没有结果或者不正确不完整尝试【可靠解】 b.读头有存储和验证合法UID号，需要把UID号设置成原卡一样才可以 c.需要多刷几次，一般情况两次以上的交互即可解算。 d.读头可能快速验证了多个扇区，这种情况只能获取到首个扇区秘钥。 c.读头并未发出密码访问，仅仅读了UID号   ![](http://blog.echo.cool/wp-content/uploads/2018/07/1.从卡扣处掰开取出电路板-1024x606.png) ![](http://blog.echo.cool/wp-content/uploads/2018/07/2.贴膜-571x1024.png) ![](http://blog.echo.cool/wp-content/uploads/2018/07/3.安装电池，电池有字一面朝上插入.png)