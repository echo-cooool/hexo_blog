---
title: '[学习笔记] TensorFlow 入门之基本使用'
tags:
  - ML
url: 11684.html
id: 11684
categories:
  - 机器学习
date: 2018-04-19 22:21:17
---

[\[学习笔记\] TensorFlow 入门之基本使用](http://www.cnblogs.com/flyu6/p/5555161.html)
==========================================================================

### 整体介绍

使用 TensorFlow, 你必须明白 TensorFlow:

*   使用图 (graph) 来表示计算任务.
*   在被称之为 会话 (Session) 的上下文 (context) 中执行图.
*   使用 tensor 表示数据.
*   通过 变量 (Variable) 维护状态.
*   使用 feed 和 fetch 可以为任意的操作(arbitrary operation)

赋值或者从其中获取数据.

一个 TensorFlow 图描述了计算的过程. 为了进行计算, 图必须在 会话 里被启动. 会话 将图的 op 分发到诸如 CPU 或 GPU 之类的 设备 上, 同时提供执行 op 的方法. 这些方法执行后, 将产生的 tensor 返回. 在 Python 语言中, 返回的 tensor 是 numpy ndarray 对象; 在 C 和 C++ 语言中, 返回的 tensor 是tensorflow::Tensor 实例.

### 计算图

TensorFlow 程序通常被组织成一个构建阶段和一个执行阶段. 在构建阶段, op 的执行步骤 被描述成一个图. 在执行阶段, 使用会话执行执行图中的 op.

其实这就是一个声明式编程结构，就好比炒菜，我们都是把主材和佐料就准备好，才添油烹制。tensorflow的计算方式也是如此，我们先在构建阶段将这个网络（如神经网络）构建出来，然后我们使用TensorFlow提供的Session方法开启一个运行（run()）将我们的网络放进去run一下，就可以得到我们想到的结果。这就是声明式的编程方式。

> Step 1： 构建图

    import tensorflow as tf
    # 创建一个常量 op, 产生一个1x2 矩阵这个op被称作是一个节点
    # 加到默认图中
    #
    #构造器的返回值代表常量 op的返回值
    a = tf.constant([[3., 3.]])
    
    b = tf.constant([[2.],[2.])
    
    # 创建一个矩阵乘法操作， a, b作为输入
    # 返回 product 代表乘法的结果
    product = tf.matmul(a,b)

现在已经创建好了一个 两个矩阵相乘并返回product结果的图。也就是说主材和佐料已经准备好了。接下来就是到了生火炒菜的时间了。为了得到product，我们就必须在一个会话（Session）中启动这个一个图了。

> Step 2：启动一个图

    #接着上面的代码
    sess = tf.Session()
    
    # 调用 sess 的 'run()' 方法来执行矩阵乘法 op, 传入 'product' 作为该方法的参数. 
    # 上面提到, 'product' 代表了矩阵乘法 op 的输出, 传入它是向方法表明, 我们希望取回
    # 矩阵乘法 op 的输出.
    #
    # 整个执行过程是自动化的, 会话负责传递 op 所需的全部输入. op 通常是并发执行的.
    # 
    # 函数调用 'run(product)' 触发了图中三个 op (两个常量 op 和一个矩阵乘法 op) 的执行.
    #
    # 返回值 'result' 是一个 numpy `ndarray` 对象.
    
    sess.run(product)
    print result
    
    # ==> [[12.]]
    
    # 任务完成后就需要关闭
    sess.close()

当然，在我们写代码的时候，有时候会忘记写sess.close().这里我们可以使用系统的带的with来实现session的自动关闭。

    with tf.Session() as sess:
          result = sess.run([product])
          print result

TensorFlow自从0.8版本开始支持分布式处理的机器学习，而且同时，TensorFlow会充分的利用计算机资源：cpu GPU 等。而且如果检测到GPU，会尽可能的使用GPU来实现对程序的计算。而当计算机上有多个GPU的时候，我们可以通过tf.device()来指定哪个GPU来执行。具体示例如下：

    with tf.Session() as sess:
    with tf.device("/gpu:1"):
        a = tf.constant([[3., 3.]])
        b = tf.constant([[2.],[2.])
        product = tf.matmul(a,b)
        ...

设备用字符串进行标识. 目前支持的设备包括:

*    "/cpu:0": 机器的 CPU.
*    "/gpu:0": 机器的第一个 GPU, 如果有的话.
*    "/gpu:1": 机器的第二个 GPU, 以此类推.

### 交互式使用

文档中的 Python 示例使用一个会话 Session 来 启动图, 并调用 \*\*Session.run()\*\*方法执行操作.

为了便于使用诸如 IPython 之类的 Python 交互环境, 可以使用InteractiveSession 代替 Session 类, 使用 Tensor.eval() 和 Operation.run() 方法代替 Session.run(). 这样可以避免使用一个变量来持有会话。

    # 进入一个交互式的会话
    import tensorflow as tf
    sess = tf.InteractiveSession()
    
    x = tf.Variable([1.0, 2.0])
    a = tf.constant([3.0, 3.0])
    
    # 使用初始化来初始化 Variable
    x.initializer.run()
    
    # 增加一个减法操作 sub op 从x 减去a,然后输出结果
    sub = tf.sub(x,a)
    print sub.eval()
    
    # ==> [-2 -1]

### Tensor

在TensorFlow中使用Tensor数据结构来表示所有的数据。Tensor可以看做是一个n维的数组或列表。一个Tensor包含一个静态类型Rank和一个shape.

### 变量 Variable

变量维护图执行过程中的状态信息。下面的例子演示了如何使用变量实现一个简单的计数器。

    # 创建一个变量，  初始化为标量 0
    state = tf.Variable(0, name="counter")
    
    # 创建一个operation, 其作用是使state 增加 1
    one = tf.constant(1)
    new_value = tf.add(sate,one)
    update = tf.assign(state, new_value)
    
    # 启动图后, 变量必须先经过`初始化` (init) op 初始化,
    # 首先必须增加一个`初始化` op 到图中.
    init_op = tf.initialize_all_variables()
    
    with tf.Session() as sess:
        sess.run(init_op) # 运行 init_op
        
        print sess.run(state) # 打印出事状态
        
        for _ in range(3):
        sess.run(update)
        print sess.run(state)
        
    
    # 输出:
    # 0
    # 1
    # 2
    # 3

### Fetch

为了取回操作的输出内容, 可以在使用 Session 对象的 run() 调用 执行图时, 传入一些 tensor, 这些 tensor 会帮助你取回结果. 在之前的例子里, 我们只取回了单个节点 state, 但是你也可以取回多个 tensor:

    input1 = tf.constant(3.0)
    input2 = tf.constant(2.0)
    input3 = tf.constant(5.0)
    intermed = tf.add(input2, input3)
    mul = tf.mul(input1, intermed)
    
    with tf.Session():
      result = sess.run([mul, intermed])
      print result
    
    # 输出:
    # [array([ 21.], dtype=float32), array([ 7.], dtype=float32)]

### Feed

上述示例在计算图中引入了 tensor, 以常量或变量的形式存储. TensorFlow 还提供了 feed 机制, 该机制 可以临时替代图中的任意操作中的 tensor 可以对图中任何操作提交补丁, 直接插入一个 tensor.

feed 使用一个 tensor 值临时替换一个操作的输出结果. 你可以提供 feed 数据作为 run() 调用的参数. feed 只在调用它的方法内有效, 方法结束, feed 就会消失. 最常见的用例是将某些特殊的操作指定为 "feed" 操作, 标记的方法是使用 tf.placeholder() 为这些操作创建占位符.

    input1 = tf.placeholder(tf.types.float32)
    input2 = tf.placeholder(tf.types.float32)
    output = tf.mul(input1, input2)
    
    with tf.Session() as sess:
      print sess.run([output], feed_dict={input1:[7.], input2:[2.]})
    
    # 输出:
    # [array([ 14.], dtype=float32)]

如果没有正确提供 feed, placeholder() 操作将会产生错误.