---
layout: post
title:  "我的第一个机器学习实例"
date:   2017-10-17 20:17:50 +0800
category: tech
---
![Tensorflow](https://i.ytimg.com/vi/qTZMWB6Fw0g/maxresdefault.jpg)

### 源码

```
import tensorflow as tf
import numpy as np

# create data
x_data = np.random.rand(100).astype(np.float32)
y_data = x_data*0.1 + 0.3

# create tensorflow structure start #
Weights = tf.Variable(tf.random_uniform([1], -1.0, 1.0))
biases = tf.Variable(tf.zeros([1]))

y = Weights*x_data + biases

loss = tf.reduce_mean(tf.square(y-y_data))

# 0.5 学习效率
optimizer = tf.train.GradientDescentOptimizer(0.5)
train = optimizer.minimize(loss)

init = tf.initialize_all_variables()
# create tensorflow structure end #

sess = tf.Session()
sess.run(init) # Very important

for step in range(201):
    sess.run(train)
    if step % 20 == 0:
        print(step, sess.run(Weights), sess.run(biases))

```

### 结果

```
0 [-0.19921991] [ 0.68492019]
20 [-0.01032349] [ 0.36265659]
40 [ 0.06891425] [ 0.3176547]
60 [ 0.09124101] [ 0.30497456]
80 [ 0.097532] [ 0.30140167]
100 [ 0.09930458] [ 0.30039495]
120 [ 0.09980403] [ 0.30011129]
140 [ 0.09994479] [ 0.30003136]
160 [ 0.09998443] [ 0.30000886]
180 [ 0.09999561] [ 0.30000252]
200 [ 0.09999878] [ 0.3000007]

```

[实例视频](https://www.youtube.com/watch?v=JKR1Dxinwwc&index=8&list=PLXO45tsB95cKI5AIlf5TxxFPzb-0zeVZ8)


另外利用RNN解析图片， 一般都会用到MNIST这个手写数字的数据集，这里再补充一点关于图像的基本概念。

#### 像素（pixel)
電腦上的影像是利用影像的小方格就是所謂的「像素」（Pixel）所構成的，這些小方格是影像中最小的單位，每一個小方格都有一個明確的位置，和單一的色彩，而這些一格格的位置和色彩就決定了該影像所呈現出來的樣子

#### 解析度（Resolution）
所謂解析度，指的是單位長度上像素的數目，單位可分「像素／英吋」或是「像素／公分」（pixels/inch；pixels/cm）。解析度的設定是決定列印品質的重要因素，高解析度的影像運用較多的像素，所以可呈現出比低解析度影像更細膩的色調變化，相對的檔案體積也更大。

