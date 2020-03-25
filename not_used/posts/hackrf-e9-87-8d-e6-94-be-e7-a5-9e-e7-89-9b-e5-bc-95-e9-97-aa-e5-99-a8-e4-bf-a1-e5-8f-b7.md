---
title: HackRF重放神牛引闪器信号
tags:
  - Good
  - SDR
url: 13629.html
id: 13629
categories:
  - SDR
date: 2018-05-12 22:24:01
---

这一次我们重放无线引闪器的信号。

0x01 找信号
--------

\[caption id="attachment_14467" align="alignnone" width="300"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-57.jpg) \[/caption\]\[caption id="attachment_14468" align="alignnone" width="150"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-58.jpg) \[/caption\]\[caption id="attachment_14469" align="alignnone" width="225"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-59.jpg) \[/caption\] 我们可以看到，其无线工作频率为2.4Ghz，所以和以前一样，使用URH进行录制和重放。

0x02 录制
-------

\[caption id="attachment_14470" align="alignnone" width="300"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-60.jpg) \[/caption\]

0x03 分析
-------

这次我们重在分析。 发射时，我把引闪器的**闪光手动调为1/32的功率**。 这次的信号和直线抓取到无线门铃的信号大有不同，信号明显被分成了两段。所以有必要进一步分析一下。 首先，我们看前面的第一段。 \[caption id="attachment_14471" align="alignnone" width="300"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-61.jpg) \[/caption\] 我们将其他部分删去，之重放这一小段，发现闪光灯会闪光，但是**并没有将闪光功率调整为我设置1/32的功率。** 所以后面那一段的功能自然浮出水面。 \[caption id="attachment_14472" align="alignnone" width="300"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/unnamed-file-62.jpg) \[/caption\] 这一次，我们只重放后面的这一段，果然闪光灯**没有闪光**，而功率被调整到了1/32。 至此我们可以得出结论前半部分的闪光仅仅是起到快速触发闪光的功能，而设置信息是后同步过去的。

0x04 建议
-------

我建议厂商能加入**时序码**之类的校验信息这样就可以避免被重放攻击所控制。