---
title: Python-with 上下文管理器
tags:
  - python
url: 14309.html
id: 14309
categories:
  - Python
date: 2018-05-24 13:09:25
---

这里我们说一下Python中的上下文管理器。 虽然名字很高大上，但是实际理解起来并不繁琐。之前在Tensorflow的文章中曾经也使用到了With作为**上下文管理器**。 其实他就像一个容器，在上下文管理器中的程序会在这样一个容器中运行，当退出时With会清空掉所有使用过的内容，并且对没有保存的文件进行保存。 如果不用with语句，代码如下：

file = open("/tmp/foo.txt")
data = file.read()
file.close()

这里有两个问题: 一是可能忘记关闭文件句柄； 二是文件读取数据发生异常，没有进行任何处理。 我们当然可以手动处理异常：

try:
    f = open('xxx')
except:
    print 'fail to open'
    exit(-1)
try:
    do something
except:
    do something
finally:
     f.close()

但明显**太繁琐**了。 所以我们这样操作： ![](http://blog.echo.cool/wp-content/uploads/2018/05/捕获-1.png) 这里我们就使用了With打开文件，这样就可以省去Flie.Close()的操作 with只有特定场合下才能使用。，这个特定场合只的是那些支持了上下文管理器的对象。 这些对象有：

1 file
2 decimal.Context
3 thread.LockType
4 threading.Lock
5 threading.RLock
6 threading.Condition
7 threading.Semaphore
8 threading.BoundedSemaphore