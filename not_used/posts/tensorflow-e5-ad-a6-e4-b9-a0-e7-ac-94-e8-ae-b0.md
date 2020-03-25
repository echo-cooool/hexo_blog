---
title: Tensorflow-学习笔记
tags:
  - Good
  - ML
url: 13506.html
id: 13506
categories:
  - 机器学习
date: 2018-04-21 17:15:09
---

最近学习了一下Google的开源机器学习框架，简单写一下自己对于MNIST学习过程的理解

1
2
3
4

import tensorflow as tf
from tensorflow.examples.tutorials.mnist import input_data
import argparse
import sys

这里的几行分别包含了Tensorflow的库和学习所需要的包（并非重点） \[video width="960" height="480" mp4="https://x.wangyuyang.top/wp-content/uploads/2018/05/417891355daafa60ab0ffac6769c485c.mp4"\]\[/video\]

1
2
3
4
5
6

FLAGS = None
parser = argparse.ArgumentParser()
parser.add_argument('--data_dir', type=str, default='/tmp/tensorflow/mnist/input_data',
 help='Directory for storing input data')
FLAGS, unparsed = parser.parse\_known\_args()
mnist = input\_data.read\_data\_sets(FLAGS.data\_dir, one_hot=True)

这里将数据下载到本地的/tmp/tensorflow下以便机器学习的时候使用

1
2

x = tf.placeholder("float",\[None,784\])
W = tf.Variable(tf.zeros(\[784,10\]))

首先以占位符的形式定义了x这一**张量**，x拥有两个维度，第一个维度我们设为None，因为我们需要读取图片，并将其的顺序放在第一个维度上，第二个维度拥有784个数，也就是789个像素，这样就可以完成数据的读取。 ![](http://blog.echo.cool/wp-content/uploads/2018/05/tensorflow-学习笔记-6.png) 之后我们定义了W这一权重值，这里有可能会理解错。w在第一个维度上有784个数字，也就是对应每一位都有对应的权重，第二个维度是分类。我们要将0~9这些数字分成十类分别进行加权求和，所以定义这样一个张量。

1
2
3

b = tf.Variable(tf.zeros(\[10\]))
y = tf.nn.softmax(tf.matmul(x,W) + b )
y_ = tf.placeholder("float",\[None,10\]) 

![](http://blog.echo.cool/wp-content/uploads/2018/05/tensorflow-学习笔记-7.png) 下面我们又定义了b作为偏置或者称为修正值，类似一次函数。 之后，我们让y作为运算结果，让x和W进行矩阵相乘，最后分别加上修正值b。再对计算后的结果进行Softmax回归运算，这样我们就可以得到输入图片对应每一个类的可能性。 ![](http://blog.echo.cool/wp-content/uploads/2018/05/tensorflow-学习笔记-8.png) ![](http://blog.echo.cool/wp-content/uploads/2018/05/tensorflow-学习笔记-9.png)

1
2
3
4
5
6
7
8
9
10
11
12
13

cross\_entropy = -tf.reduce\_sum(y_ * tf.log(y))
train_step = tf.train.GradientDescentOptimizer(0.01).minimize(cross_entropy)
init = tf.global\_variables\_initializer()
sess = tf.Session()
sess.run(init)
for i in range(10000):
 batch\_xs, batch\_ys = mnist.train.next_batch(50)

 sess.run(train\_step, feed\_dict={x: batch\_xs, y\_: batch_ys})

correct_prediction = tf.equal(tf.argmax(y,1), tf.argmax(y_,1))
accuracy = tf.reduce\_mean(tf.cast(correct\_prediction, "float"))
print str(sess.run(accuracy, feed\_dict={x: mnist.test.images, y\_: mnist.test.labels})*100) \+ "%"

训练模型
----

为了训练我们的模型，我们首先需要定义一个指标来评估这个模型是好的。其实，在机器学习，我们通常定义指标来表示一个模型是坏的，这个指标称为成本（cost）或损失（loss），然后尽量最小化这个指标。但是，这两种方式是相同的。 一个非常常见的，非常漂亮的成本函数是“交叉熵”（cross-entropy）。交叉熵产生于信息论里面的信息压缩编码技术，但是它后来演变成为从博弈论到机器学习等其他领域里的重要技术手段。它的定义如下： ![](http://blog.echo.cool/wp-content/uploads/2018/05/tensorflow-学习笔记-10.png) 下面我们要求使用**梯度下降算法**降低loss（交叉熵）并且每次读取50个数字并循环10000次。 最后输出评估结果，大约在92%左右 **2018.4.24** OK已完成数据可视化： ![](http://blog.echo.cool/wp-content/uploads/2018/05/tensorflow-学习笔记-11.png)![](http://blog.echo.cool/wp-content/uploads/2018/05/tensorflow-学习笔记-12.png)![](http://blog.echo.cool/wp-content/uploads/2018/05/tensorflow-学习笔记-13.png)![](http://blog.echo.cool/wp-content/uploads/2018/05/tensorflow-学习笔记-14.png)![](http://blog.echo.cool/wp-content/uploads/2018/05/tensorflow-学习笔记-15.png)![](http://blog.echo.cool/wp-content/uploads/2018/05/tensorflow-学习笔记-16.png) 目前国内的机器学习资料还是比较少，大部分还是Google上的英文资料，毕竟新技术嘛。 快高三了，这些可能要大学再搞了。