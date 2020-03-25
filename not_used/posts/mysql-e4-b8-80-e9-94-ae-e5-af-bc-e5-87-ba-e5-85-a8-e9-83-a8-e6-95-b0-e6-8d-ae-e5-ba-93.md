---
title: MySQL一键导出全部数据库
url: 15088.html
id: 15088
categories:
  - Computer
date: 2019-02-21 19:09:35
tags:
---

导出全部数据库，再把数据库恢复回来，其实利用`mysqldump`的`—all-databases`参数可以一口气把你数据库`root`用户下的所有数据库一口气导出到一个sql文件里。然后，重装系统后使用`source`命令可以再一口气倒回来。 导出全部数据库`mysqldump -uroot -p --all-databases > sqlfile.sql`

此操作会把数据库服务器root用户下的所有数据库都导出来。 如果回车后提示Enter Password：请输入你的mysql root密码.

![](http://blog.echo.cool/wp-content/uploads/2019/02/mysql一键导出全部数据库.png)

注意：all前面是两个减号（-），`databases`前面是一个减号 `--all-databases` 像上图那样操作，就会在我的d盘生成一个sqlfile.sql文件，导出过程中没有光标闪烁，当你发现又可以键入命令（有光标闪烁了），数据库就导出完成了.

吼吼，还不小呢。 导入： 1.登录mysal：

    mysql–uroot –p

根据提示输入密码 ![](http://blog.echo.cool/wp-content/uploads/2019/02/mysql一键导出全部数据库-1.png) 然后：

    source sqlfile.sql;