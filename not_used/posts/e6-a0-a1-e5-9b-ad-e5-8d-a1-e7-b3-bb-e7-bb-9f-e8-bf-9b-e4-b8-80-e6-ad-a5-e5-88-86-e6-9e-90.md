---
title: 校园卡系统进一步分析
tags:
  - Good
  - 学校
url: 13853.html
id: 13853
categories:
  - 安全测试
date: 2018-05-15 22:24:01
---

0x01
----

在上次的分析过后，我们将进一步分析一下校园卡的刷卡系统安全隐患。毕竟除了充值系统，**校园一卡通**还是有很多应用场景的。

0x02 分析
-------

我们使用Proxmark3读取一张校园一卡通。 \[caption id="attachment_14266" align="alignnone" width="225"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/校园卡系统进一步分析.jpg) \[/caption\]\[caption id="attachment_14267" align="alignnone" width="300"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/校园卡系统进一步分析-1.jpg) \[/caption\] 可以看到，校园一卡通的卡片只有第一行存在数据，也就是说刷卡机和门禁系统**只校验卡片的UID**来判别身份。 的确，这样让开发系统时极大的减小了负担，但同样也具有极大的安全风险。 进一步读取卡类型： \[caption id="attachment_14268" align="alignnone" width="225"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/校园卡系统进一步分析-2.jpg) \[/caption\] \[caption id="attachment_14269" align="alignnone" width="300"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/校园卡系统进一步分析-3.jpg) \[/caption\] 可以知道，校园IC卡使用了**NXP MIFARE CLASSIC技术，卡片大小Plus 2k SL1共16扇区。** 科普一下IC卡原理中的UID部分：

> [IC卡](https://baike.baidu.com/item/IC%E5%8D%A1) (Integrated Circuit Card，集成电路卡)，也称智能卡(Smart card)、智慧卡(Intelligent card)、微电路卡(Microcircuit card)或微芯片卡等。它是将一个[微电子](https://baike.baidu.com/item/%E5%BE%AE%E7%94%B5%E5%AD%90)[芯片](https://baike.baidu.com/item/%E8%8A%AF%E7%89%87)嵌入符合ISO 7816标准的[卡基](https://baike.baidu.com/item/%E5%8D%A1%E5%9F%BA)中，做成卡片形式。IC卡与读写器之间的通讯方式可以是[接触](https://baike.baidu.com/item/%E6%8E%A5%E8%A7%A6/5692)式，也可以是非接触式。根据通讯接口把IC卡分成接触式IC卡、非接触式IC和[双界面卡](https://baike.baidu.com/item/%E5%8F%8C%E7%95%8C%E9%9D%A2%E5%8D%A1)（同时具备接触式与非接触式通讯接口）。 UID卡片完全兼容mifare 1k卡片。卡片的b**lock0（UID所在的block）可以任意修改**，重复修改。block0直接用普通mifare读写器修改，不需要特殊设备。卡片的默认密码为12个F，即FFFFFFFFFFFF。 **密码破解的几种方法：** 1）密钥列表当中的12个0是不存在的，还有就是16进制有Z的吗？看来是我土了！ 2）关于认证嵌套漏洞，这个因为作者文章忽略了权限的部分，所以我可否忽略？因为没有权限，何来认证嵌套漏洞呢？ 3）DarkSide攻击，仅仅是基于IC卡类别当中NXP公司所发布的MIFARE CLASSIC系列（S50/S70）而不是所有的IC卡！文中没有说明问题究竟是存在于哪里，我也曾经说过关于这个方面的问题，什么是PRNG漏洞，以及PRNG漏洞和WEP的关系！所以不再多说 4）正常验证过程获取Key，首先SAM并非是正常，而是在不安全的对称性算法当中增加了一个安全模块，去加密彼此之间的通信安全，但就是基于读卡器返回的数值是明文而存在了关于监听攻击的内容，文中好像把我之前关于SAM部分非监听部分的内容拿出来说之后，而没有注意究竟问题是什么！

这里我们就采用**UID卡**。

0x03 复制
-------

\[caption id="attachment_14270" align="alignnone" width="300"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/校园卡系统进一步分析.png) \[/caption\] 我们分析数据的**CardCode字段**。发现其正好是**UID的十六进制倒序**。所以写一个小程序(Python)来做转换。

x = input("ID:\\n")
a = hex(x)
UID = a\[8\]+a\[9\] + a\[6\]+a\[7\] + a\[4\]+a\[5\] + a\[2\]+a\[3\]
print UID

\[caption id="attachment_14271" align="alignnone" width="300"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/校园卡系统进一步分析-4.jpg) \[/caption\] \[caption id="attachment_14272" align="alignnone" width="300"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/校园卡系统进一步分析-5.jpg) \[/caption\] 顺便再拿出八百年前的校验码计算器： \[caption id="attachment_14273" align="alignnone" width="300"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/校园卡系统进一步分析-6.jpg) \[/caption\] 好了。现在，可以复制了。 我们将修改后数据填入Proxmark3上位机内，克隆至UID卡。完工。

0x04 测试
-------

\[caption id="attachment_14275" align="alignnone" width="225"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/校园卡系统进一步分析-8.jpg) \[/caption\]\[caption id="attachment_14277" align="alignnone" width="225"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/校园卡系统进一步分析-10.jpg) \[/caption\] 拿到大叔面前： \[caption id="attachment_14279" align="alignnone" width="225"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/校园卡系统进一步分析-12.jpg) \[/caption\] \[caption id="attachment_14281" align="alignnone" width="225"\]![](http://blog.echo.cool/wp-content/uploads/2018/05/校园卡系统进一步分析-14.jpg) \[/caption\] **7774.0   嗯。**

0x05 建议
-------

至此，我们完成了一项并不十分友好的工作。 当然，永远不要忘记权力赋予的**责任**。我们并非想要获得某些利益。 我们希望学校能够更好的发展，当然，在安全的情况下。 我希望，学校能够升级饭卡管理系统，不单单使用UID进行身份识别。同样，在KeyA和KeyB的设置上增大随机性，以此达到更好的安全性。