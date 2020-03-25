---
title: wordpress网站配置微信小程序
tags:
  - wordpress
url: 14073.html
id: 14073
categories:
  - Wordpress
date: 2018-05-19 21:19:30
---

小程序正在审核中，很快就要上线了~ ![](http://blog.echo.cool/wp-content/uploads/2018/05/wordpress网站配置微信小程序.jpg)![](http://blog.echo.cool/wp-content/uploads/2018/05/wordpress网站配置微信小程序-1.jpg) 这里比较大的一个坑就是配置https，比较繁琐。 首先，在宝塔界面申请SSL证书![](http://blog.echo.cool/wp-content/uploads/2018/05/wordpress网站配置微信小程序-2.jpg)。 在Dashboard修改域名之后，访问网站会出现排版错误，需要在Config.php中加入一行

$_SERVER\['HTTPS'\] = 'on';
define('FORCE\_SSL\_LOGIN', true);
define('FORCE\_SSL\_ADMIN', true);

这样就可以让网站，支持https。 当然这样就让网站出现了一些问题，本来是域名 blog.echo.cool 但是微信小程序必须使用已备案域名，所以换为了x.wangyuyang.top 也就是说，还要重新收录啊，，，， 2018.5.21 发现一个问题： ![](http://blog.echo.cool/wp-content/uploads/2018/05/wordpress网站配置微信小程序-3.jpg) 审核总是出一些莫名其妙的问题，本来打开的很好啊。。 终于，一次不小心打开的详情 ![](http://blog.echo.cool/wp-content/uploads/2018/05/wordpress网站配置微信小程序-4.jpg) 应该是基础调试库的问题了，，改一下，再提交审核 ![](http://blog.echo.cool/wp-content/uploads/2018/05/wordpress网站配置微信小程序-5.jpg) 这一次应该就不会有问题了。 2018.5.22 ![](http://blog.echo.cool/wp-content/uploads/2018/05/wordpress网站配置微信小程序.png)