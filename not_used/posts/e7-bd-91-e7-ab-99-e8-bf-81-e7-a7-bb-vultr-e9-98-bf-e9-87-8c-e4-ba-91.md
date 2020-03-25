---
title: 网站迁移 Vultr-阿里云
tags:
  - web
url: 14091.html
id: 14091
categories:
  - Wordpress
date: 2018-05-22 22:46:54
---

主要是为了适配小程序，但由于GFW让国外Vultr上的网站间歇性抽风。 同时也为了速度，将网站迁移到阿里云 这里有一些遇到的坑，记一下～

首先是WordPress迁移后404的问题：
----------------------

这个主要是因为固定链接和伪静态设置错误造成的。 网站原来是域名+index.php/+文章日期/文章名称 但是迁移之后，会造成固定链接失效。 解决方法： 1，.htaccess要开放写权限。这样在自己定义wp的永久链接时，wp会自己主动重写.htaccess。所谓删除或手动重写.htaccess就是由于没有开放它的写权限。 2，进入后台，选择固定链接选项，从新提交一次设置很可能就好了啦。 3，设置伪静态 ![](http://blog.echo.cool/wp-content/uploads/2018/05/自动草稿-3.jpg)

location / {
	index index.html index.php; 
	if (-f $request_filename/index.html){ 
		rewrite (.*) $1/index.html break; 
	} 
	if (-f $request_filename/index.php){ 
		rewrite (.*) $1/index.php; 
	} 
	if (!-f $request_filename){ 
		rewrite (.*) /index.php; 
	} 
} 

rewrite /wp-admin$ $scheme://$host$uri/ permanent;

之后是SSL的问题：
----------

因为要配置小程序，需要https，所以还需要配置ssl ![](http://blog.echo.cool/wp-content/uploads/2018/05/自动草稿-4.jpg) 这里生成的证书，如果要部署CDN的话还需要在CDN界面重新输入。 2018.5.23 重新迁移回Vultr在国内的阿里云，这么好的域名就废了。