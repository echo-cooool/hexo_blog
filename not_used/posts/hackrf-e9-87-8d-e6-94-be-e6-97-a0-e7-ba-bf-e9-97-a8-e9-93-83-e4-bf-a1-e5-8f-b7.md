---
title: HackRF重放无线门铃信号
tags:
  - Good
  - SDR
url: 13628.html
id: 13628
categories:
  - SDR
date: 2018-05-12 22:23:40
---

我们这里同样使用URH进行实验

0x00 软件安装
---------

Linux：

    sudo apt-get update
    sudo apt-get install python3-numpy python3-psutil python3-zmq python3-pyqt5 g++ libpython3-dev python3-pip
    sudo pip3 install urh
    

启动软件直接在shell里输入

    urh

即可启动软件 Windows： [https://github.com/jopohl/urh/releases](https://github.com/jopohl/urh/releases) 在上面的地址中，下载最新版的.msi安装文件安装即可。 注意Windows下还需要安装驱动： 下载[Zadig](http://sourceforge.net/projects/libwdi/files/zadig/) 用7zip解压之后，执行Zadig即可 \[caption id="attachment\_13544" align="alignnone" width="300"\]\[caption id="attachment\_14474" align="alignnone" width="300"\]![zadig-300x136.jpg](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-63.jpg) zadig-300x136.jpg\[/caption\] zadig-300x136.jpg\[/caption\] 注意选择你的HackRF设备。

0x01 寻找信号源频率
------------

打开SDR#，根据淘宝商品页的信息 \[caption id="attachment_14475" align="alignnone" width="150"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-18.png) \[/caption\] 我们猜测其工作频率应该在433Mzh，果不其然： \[caption id="attachment_14476" align="alignnone" width="300"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-64.jpg) \[/caption\]

0x02 录制
-------

\[caption id="attachment_14477" align="alignnone" width="288"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-65.jpg) \[/caption\]配置参数 \[caption id="attachment_14478" align="alignnone" width="300"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-66.jpg) \[/caption\]

0x03 重放
-------

\[caption id="attachment_14479" align="alignnone" width="300"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-67.jpg) \[/caption\]\[caption id="attachment_14480" align="alignnone" width="300"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-68.jpg) \[/caption\] 我们首先选择了一段信号，之后点击Send Data 发送即可。果然，门铃响了起来。

0x04 分析
-------

\[caption id="attachment_14481" align="alignnone" width="300"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-69.jpg) \[/caption\] 我们将信号导入分析器，但貌似这次的信号没有规律。 所以文章就到这里吧，下次我们再进行分析。可以参见神牛闪光的那篇文章。