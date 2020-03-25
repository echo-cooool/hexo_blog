---
title: Tensorflow-学习笔记
url: 14934.html
id: 14934
categories:
  - Computer
  - 机器学习
date: 2018-08-10 21:49:16
tags:
---

最近学习了一下Google的开源机器学习框架，简单写一下自己对于MNIST学习过程的理解 最终结果如下： ![](http://blog.echo.cool/wp-content/uploads/2018/08/tensorflow-学习笔记.gif) ![](http://blog.echo.cool/wp-content/uploads/2018/08/tensorflow-学习笔记.png) ![](http://blog.echo.cool/wp-content/uploads/2018/08/tensorflow-学习笔记.jpg) ![](http://blog.echo.cool/wp-content/uploads/2018/08/tensorflow-学习笔记-1.jpg) 我们针对MNIST数据集进行学习 MNIST是一个入门级的计算机视觉数据集，它包含各种手写数字图片： ![](http://blog.echo.cool/wp-content/uploads/2018/08/tensorflow-学习笔记-2.jpg) ![](http://blog.echo.cool/wp-content/uploads/2018/08/tensorflow-学习笔记-1.gif) ![](http://blog.echo.cool/wp-content/uploads/2018/08/tensorflow-学习笔记-1.png) 它也包含每一张图片对应的标签，告诉我们这个是数字几。比如，上面这四张图片的标签分别是5，0，4，1。

MNIST数据集
--------

下载数据：

    import tensorflow.examples.tutorials.mnist.input_data as input_data
    mnist = input_data.read_data_sets(MNIST_data/, one_hot=True)

下载下来的数据集被分成两部分：60000行的训练数据集（`mnist.train`）和10000行的测试数据集（`mnist.test`）。这样的切分很重要，在机器学习模型设计时必须有一个单独的测试数据集不用于训练而是用来评估这个模型的性能，从而更加容易把设计的模型推广到其他数据集上（泛化）。 正如前面提到的一样，每一个MNIST数据单元有两部分组成：一张包含手写数字的图片和一个对应的标签。我们把这些图片设为“xs”，把这些标签设为“ys”。训练数据集和测试数据集都包含xs和ys，比如训练数据集的图片是 `mnist.train.images` ，训练数据集的标签是 `mnist.train.labels`。 每一张图片包含28X28个像素点。我们可以用一个数字数组来表示这张图片： ![](http://blog.echo.cool/wp-content/uploads/2018/08/tensorflow-学习笔记-3.jpg) 我们把这个数组展开成一个向量，长度是 28x28 = 784。如何展开这个数组（数字间的顺序）不重要，只要保持各个图片采用相同的方式展开。从这个角度来看，MNIST数据集的图片就是在784维向量空间里面的点, 并且拥有比较复杂的结构 (提醒: 此类数据的可视化是计算密集型的)。 展平图片的数字数组会丢失图片的二维结构信息。这显然是不理想的，最优秀的计算机视觉方法会挖掘并利用这些结构信息，我们会在后续教程中介绍。但是在这个教程中我们忽略这些结构，所介绍的简单数学模型，softmax回归(softmax regression)，不会利用这些结构信息。 因此，在MNIST训练数据集中，`mnist.train.images` 是一个形状为 `[60000, 784]` 的张量，第一个维度数字用来索引图片，第二个维度数字用来索引每张图片中的像素点。在此张量里的每一个元素，都表示某张图片里的某个像素的强度值，值介于0和1之间。 ![](http://blog.echo.cool/wp-content/uploads/2018/08/tensorflow-学习笔记-4.jpg) 相对应的MNIST数据集的标签是介于0到9的数字，用来描述给定图片里表示的数字。为了用于这个教程，我们使标签数据是one-hot vectors。 一个one-hot向量除了某一位的数字是1以外其余各维度数字都是0。所以在此教程中，数字n将表示成一个只有在第n维度（从0开始）数字为1的10维向量。比如，标签0将表示成(\[1,0,0,0,0,0,0,0,0,0,0\])。因此， `mnist.train.labels` 是一个 `[60000, 10]` 的数字矩阵。 ![](http://blog.echo.cool/wp-content/uploads/2018/08/tensorflow-学习笔记-2.png)

Softmax回归介绍
-----------

我们知道MNIST的每一张图片都表示一个数字，从0到9。我们希望得到给定图片代表每个数字的概率。比如说，我们的模型可能推测一张包含9的图片代表数字9的概率是80%但是判断它是8的概率是5%（因为8和9都有上半部分的小圆），然后给予它代表其他数字的概率更小的值。 下面的图片显示了一个模型学习到的图片上每个像素对于特定数字类的权值。红色代表负数权值，蓝色代表正数权值。 ![](http://blog.echo.cool/wp-content/uploads/2018/08/微信图片_20180811171249-1024x514.jpg) 我们也需要加入一个额外的偏置量（bias），因为输入往往会带有一些无关的干扰量。因此对于给定的输入图片 x 它代表的是数字 i 的证据可以表示为 ![](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==) ![](http://blog.echo.cool/wp-content/uploads/2018/08/tensorflow-学习笔记-3.png) 其中 ![](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)代表权重， ![](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==) 代表数字 i 类的偏置量，j 代表给定图片 x 的像素索引用于像素求和。 我们也可以用向量表示这个计算过程：用矩阵乘法和向量相加。这有助于提高计算效率。（也是一种更有效的思考方式） ![](http://blog.echo.cool/wp-content/uploads/2018/08/tensorflow-学习笔记-6.jpg) 更进一步，可以写成更加紧凑的方式： ![](http://blog.echo.cool/wp-content/uploads/2018/08/tensorflow-学习笔记-4.png)

实现回归模型：
-------

    <pre class="brush:python">import tensorflow as tf
    from tensorflow.examples.tutorials.mnist import input_data
    import argparse
    import sys

这里的几行分别包含了Tensorflow的库和学习所需要的包

    FLAGS = None
    parser = argparse.ArgumentParser()
    parser.add_argument('--data_dir', type=str, default='/tmp/tensorflow/mnist/input_data',
                          help='Directory for storing input data')
    FLAGS, unparsed = parser.parse_known_args()
    mnist = input_data.read_data_sets(FLAGS.data_dir, one_hot=True)

这里将数据下载到本地的/tmp/tensorflow下以便机器学习的时候使用

    x = tf.placeholder(float,[None,784])
    W = tf.Variable(tf.zeros([784,10]))

首先以占位符的形式定义了x这一张量，x拥有两个维度，第一个维度我们设为None，因为我们需要读取图片，并将其的顺序放在第一个维度上，第二个维度拥有784个数，也就是789个像素，这样就可以完成数据的读取。 之后我们定义了W这一**权重值**，这里有可能会理解错。w在第一个维度上有784个数字，也就是对应每一位都有对应的权重，第二个维度是分类。我们要将0~9这些数字分成十类分别进行加权求和，所以定义这样一个张量。

    b = tf.Variable(tf.zeros([10]))
    y = tf.nn.softmax(tf.matmul(x,W) + b )
    y_ = tf.placeholder(float,[None,10])

下面我们又定义了b作为偏置或者称为修正值，类似一次函数。 之后，我们让y作为运算结果，让x和W进行矩阵相乘，最后分别加上修正值b。再对计算后的结果进行Softmax回归运算，这样我们就可以得到输入图片对应每一个类的可能性.

    cross_entropy = -tf.reduce_sum(y_ * tf.log(y))
    train_step = tf.train.GradientDescentOptimizer(0.01).minimize(cross_entropy)
    init = tf.global_variables_initializer()
    sess = tf.Session()
    sess.run(init)
    for i in range(10000):
      batch_xs, batch_ys = mnist.train.next_batch(50)
      sess.run(train_step, feed_dict={x: batch_xs, y_: batch_ys})
    correct_prediction = tf.equal(tf.argmax(y,1), tf.argmax(y_,1))
    accuracy = tf.reduce_mean(tf.cast(correct_prediction, float))
    print str(sess.run(accuracy, feed_dict={x: mnist.test.images, y_: mnist.test.labels})*100) + %

下面我们要求使用梯度下降算法降低loss（交叉熵）并且每次读取50个数字并循环10000次。 最后输出评估结果，大约在92%左右 ![](http://blog.echo.cool/wp-content/uploads/2018/08/tensorflow-学习笔记-5.jpg) 交叉熵： ![](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)![](http://blog.echo.cool/wp-content/uploads/2018/08/tensorflow-学习笔记-2.gif)