---
title: 使用URH（Universal Radio Hacker）进行Hackrf无线重放和分析
tags:
  - Good
  - SDR
url: 13524.html
id: 13524
categories:
  - SDR
date: 2018-05-12 08:13:12
---

项目地址:[https://github.com/jopohl/urh](https://github.com/jopohl/urh) \[caption id="attachment\_13535" align="alignnone" width="690"\]\[caption id="attachment\_14488" align="alignnone" width="690"\]![Capture.JPG](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-72.jpg) Capture.JPG\[/caption\] Capture.JPG\[/caption\]

0000 HackRF 是什么？
----------------

HackRF就像是一个录音机，可以采集声音（无线电）信号，并且发送（播放）声音（无线电）信号~附HackRF的[原理图](http://www.witimes.com/wp-content/uploads/2014/06/HackRF-Schematic.pdf)： \[caption id="attachment\_13537" align="alignnone" width="690"\]\[caption id="attachment\_14489" align="alignnone" width="690"\]![image.png](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-73.jpg) image.png\[/caption\] image.png\[/caption\] \[caption id="attachment\_13539" align="alignnone" width="690"\]\[caption id="attachment\_14490" align="alignnone" width="690"\]![image.png](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-74.jpg) image.png\[/caption\] image.png\[/caption\] 目前较为知名的三款设备分别是USRP, BladeRF和HackRF（[点击这里](https://en.wikipedia.org/wiki/List_of_software-defined_radios)查看所有软件无线电设备），其中HackRF的频率覆盖范围广，价格也相对便宜，美中不足的是仅为半双工（要不可以做一个雷达），且为USB2.0接口。

0001 简介
-------

项目是由国外的jopohl所开发，因此只有英文版本。我们知道在Linux下如果要进行Hackrf的操作，基本都是gqrx和GNU radio配合使用。前几天逛Github看到了这个项目,就在Ubuntu上装了一下试了试，发现还不错，今天发现还有Windows版本。简直爽。

0010 软件
-------

先放一个软件的截图： \[caption id="attachment\_13540" align="alignnone" width="690"\]\[caption id="attachment\_14491" align="alignnone" width="690"\]![image.png](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-75.jpg) image.png\[/caption\] image.png\[/caption\] 这里是一个之前采集的神牛闪光的引闪器的信号，如果在人多的地方高速重放这个信号，嘿嘿嘿~我们还是具体来看软件，软件最上方分了四部分，分别是Interpretation(n. 解释；翻译；演出),Analysis( n. 分析；分解；验定),Generator(n. 发电机；发生器；生产者),Simulator(n. 模拟器；假装者，模拟者)相信通过英文直译也能知道是什么意思吧，一般情况下，我们只需要第一和第二部分即可。 \[caption id="attachment\_13543" align="alignnone" width="505"\]\[caption id="attachment\_14492" align="alignnone" width="505"\]![image.png](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-76.jpg) image.png\[/caption\] image.png\[/caption\]

0011 安装
-------

Linux：

    sudo apt-get update
    sudo apt-get install python3-numpy python3-psutil python3-zmq python3-pyqt5 g++ libpython3-dev python3-pip
    sudo pip3 install urh
    

启动软件直接在shell里输入

    urh

即可启动软件 Windows： [https://github.com/jopohl/urh/releases](https://github.com/jopohl/urh/releases) 在上面的地址中，下载最新版的.msi安装文件安装即可。 注意Windows下还需要安装驱动： 下载[Zadig](http://sourceforge.net/projects/libwdi/files/zadig/) 用7zip解压之后，执行Zadig即可 \[caption id="attachment\_13544" align="alignnone" width="300"\]\[caption id="attachment\_14493" align="alignnone" width="300"\]![zadig-300x136.jpg](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-77.jpg) zadig-300x136.jpg\[/caption\] zadig-300x136.jpg\[/caption\] 注意选择你的HackRF设备。

0100 使用
-------

### 录制：

\[caption id="attachment\_13545" align="alignnone" width="546"\]\[caption id="attachment\_14494" align="alignnone" width="546"\]![image.png](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-78.jpg) image.png\[/caption\] image.png\[/caption\] 点击Record signal即可进入录制页面，选择正确的设备，点击record即可记录。 \[caption id="attachment\_13546" align="alignnone" width="690"\]\[caption id="attachment\_14495" align="alignnone" width="690"\]![image.png](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-79.jpg) image.png\[/caption\] image.png\[/caption\]

### 重放：

\[caption id="attachment\_13547" align="alignnone" width="310"\]\[caption id="attachment\_14496" align="alignnone" width="310"\]![image.png](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-80.jpg) image.png\[/caption\] image.png\[/caption\] 我们直接点击那个类似播放键的按钮，进入下面的页面： \[caption id="attachment\_13548" align="alignnone" width="690"\]\[caption id="attachment\_14497" align="alignnone" width="690"\]![image.png](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-81.jpg) image.png\[/caption\] image.png\[/caption\] 得益于强大的URH我们直接点击Start即可播放刚才的信号。

### 编辑信号：

对应录制的信号，我们需要去除不需要的部分，直接选中需要留下的部分，点击右键： \[caption id="attachment\_13549" align="alignnone" width="678"\]\[caption id="attachment\_14498" align="alignnone" width="678"\]![image.png](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-82.jpg) image.png\[/caption\] image.png\[/caption\] 点击Corp to selection 即可留下我们需要的内容。

0101 未完待续
---------

对于分析和模拟的功能我们将在下一篇文章中继续讲解，先放图，嘿嘿嘿~~~ \[caption id="attachment\_13550" align="alignnone" width="690"\]\[caption id="attachment\_14499" align="alignnone" width="690"\]![image.png](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-83.jpg) image.png\[/caption\] image.png\[/caption\] \[caption id="attachment\_13551" align="alignnone" width="690"\]\[caption id="attachment\_14500" align="alignnone" width="690"\]![image.png](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-84.jpg) image.png\[/caption\] image.png\[/caption\]