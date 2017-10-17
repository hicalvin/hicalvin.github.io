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
