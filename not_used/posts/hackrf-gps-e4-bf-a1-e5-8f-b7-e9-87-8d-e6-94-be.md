---
title: HackRF GPS信号重放
tags:
  - Good
  - SDR
url: 13627.html
id: 13627
categories:
  - SDR
date: 2018-05-12 22:20:16
---

这里我们将使用HackRF进行GPS信号的发射，请注意不要在公共场合实验发射信号，请在电磁屏蔽箱内进行本实验。 我们知道民用GPS信号工作频率在 Ghz，所以我们可以用电脑生成一个虚假的GPS信号文件，再通过HackRF发射出去，这样当设备接收到我们发射的信号，在计算自身位置的时候就会计算成为我们想要的地点。

**0x01 GPS 定位原理**
-----------------

GPS导航系统的基本原理是[测量](https://wapbaike.baidu.com/item/%E6%B5%8B%E9%87%8F)出已知位置的[卫星](https://wapbaike.baidu.com/item/%E5%8D%AB%E6%98%9F)到用户接收机之间的距离，然后综合多颗卫星的[数据](https://wapbaike.baidu.com/item/%E6%95%B0%E6%8D%AE)就可知道接收机的具体位置。要达到这一目的，[卫星](https://wapbaike.baidu.com/item/%E5%8D%AB%E6%98%9F)的位置可以根据星载时钟所记录的时间在卫星星历中查出。而用户到[卫星](https://wapbaike.baidu.com/item/%E5%8D%AB%E6%98%9F)的距离则通过记录卫星信号传播到用户所经历的时间，再将其乘以光速得到（由于大气层电离层的干扰，这一距离并不是用户与卫星之间的真实距离，而是[伪距](https://wapbaike.baidu.com/item/%E4%BC%AA%E8%B7%9D)（PR，）：当GPS卫星正常工作时，会不断地用1和0二进制码元组成的[伪随机码](https://wapbaike.baidu.com/item/%E4%BC%AA%E9%9A%8F%E6%9C%BA%E7%A0%81)（简称伪码）发射[导航电文](https://wapbaike.baidu.com/item/%E5%AF%BC%E8%88%AA%E7%94%B5%E6%96%87)。GPS系统使用的伪码一共有两种，分别是民用的[C/A码](https://wapbaike.baidu.com/item/C/A%E7%A0%81)和军用的P(Y)码。C/A码频率1.023MHz，重复周期一毫秒，码间距1微秒，相当于300m；[P码](https://wapbaike.baidu.com/item/P%E7%A0%81)频率10.23MHz，重复周期266.4天，码间距0.1微秒，相当于30m。而Y码是在P码的基础上形成的，保密性能更佳。[导航电文](https://wapbaike.baidu.com/item/%E5%AF%BC%E8%88%AA%E7%94%B5%E6%96%87)包括[卫星](https://wapbaike.baidu.com/item/%E5%8D%AB%E6%98%9F)星历、工作状况、时钟改正、电离层时延修正、大气折射修正等信息。它是从[卫星](https://wapbaike.baidu.com/item/%E5%8D%AB%E6%98%9F)信号中解调制出来，以50b/s调制在载频上发射的。[导航电文](https://wapbaike.baidu.com/item/%E5%AF%BC%E8%88%AA%E7%94%B5%E6%96%87)每个主帧中包含5个子帧每帧长6s。前三帧各10个字码；每三十秒重复一次，每小时更新一次。后两帧共15000b。[导航电文](https://wapbaike.baidu.com/item/%E5%AF%BC%E8%88%AA%E7%94%B5%E6%96%87)中的内容主要有遥测码、转换码、第1、2、3[数据块](https://wapbaike.baidu.com/item/%E6%95%B0%E6%8D%AE%E5%9D%97)，其中最重要的则为星历数据。当用户接受到[导航电文](https://wapbaike.baidu.com/item/%E5%AF%BC%E8%88%AA%E7%94%B5%E6%96%87)时，提取出[卫星](https://wapbaike.baidu.com/item/%E5%8D%AB%E6%98%9F)时间并将其与自己的时钟做对比便可得知卫星与用户的距离，再利用导航电文中的[卫星](https://wapbaike.baidu.com/item/%E5%8D%AB%E6%98%9F)星历数据推算出卫星发射电文时所处位置，用户在WGS-84大地坐标系中的位置速度等信息便可得知。 \[caption id="attachment_14483" align="alignnone" width="336"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file.jpeg) \[/caption\] \[caption id="attachment_14484" align="alignnone" width="1120"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-19.png) \[/caption\]

**0x02 生成GPS模拟信号文件**
--------------------

### 1.**下载编译gps-sdr-sim**

> $ git clone https://github.com/osqzss/gps-sdr-sim.git $ cd gps-sdr-sim $ gcc-mp-5 gpssim.c -lm -O3 -o gps-sdr-si

### **2\. RINEX星历数据下****载**

> ftp://cddis.gsfc.nasa.gov/pub/gps/data/daily/2016/brdc

访问上面的地址，随便找一个最新的即可

### **3.安装必要软件**

apt-get install gnuradio gnuradio-dev gr-osmosdr gr-osmosdr gqrx-sdr wireshark

### 5.安装外部时钟

\[caption id="attachment_14485" align="alignnone" width="300"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-70.jpg) \[/caption\] 这里的外部时钟时必须要安装的，否则发射的信号手机不认。

### 6.生成GPS信号文件

./gps-sdr-sim -e brdc3540.14n -l 66,66,100 -b 8 -d 100

0x03 实施劫持
---------

让hackrf将这个文件中的内容发射出去。 这里需要注意的是由于现在的手机基本上都采用GPS定位，基站网格定位，和Wifi定位3种方式合一，所以这里需要使手机处于飞行模式才可以。在终端输入如下命令，其中1575420000指定的是发射的频率，而2600000是采样频率：

hackrf_transfer -t gpssim.bin -f 1575420000 -s 2600000 -a 1 -x 0

\[caption id="attachment_14486" align="alignnone" width="169"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-71.jpg) \[/caption\] 这里我们可以看到，已经成功定位到我们想要的地点。

0x04 总结
-------

通过这样的一次实验，我们成功欺骗了手机的GPS。 在军事上，干扰弹的原理也大同小异。所以，国家禁止随意发射GPS信号。一旦用于非法用途，可能造成很大的损失。 就拿大疆无人机来说，如果我们伪造一个坐标，飞行器将认为自己偏离的实际的地址，这样极可能造成失控。 希望，恐怕也没法实现了：在GPS信号中加入时序码和校验码之类的信号。

（不是很懂无线电，不科学的地方欢迎指出）