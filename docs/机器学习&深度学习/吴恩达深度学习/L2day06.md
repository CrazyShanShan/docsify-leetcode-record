# 6. Optimization Algorithms

## 6.1 Mini-batch gradient descent

 **empirical: 经验** **regime: 制度** **capsule: 压缩** **connotation: 内涵**

![image-20211108193252385](../../pictures/DL6-1-1.png)

![image-20211108194025883](../../pictures/DL6-1-2.png)

## 6.2 Understanding mini-batch gradient descent 

![image-20211111133554894](../../pictures/DL6-2-1.png)

**stochastic ： 随机的** **ameliorated: 改善** **converge: 收敛** **consequent descent: 顺向** **oscillate: 震荡**

![image-20211111134452443](../../pictures/DL6-2-2.png)

## 6.3 Exponentially(指数) weighted（权值） averages（平均）

![image-20211111134847210](../../pictures/DL6-3-1.png)

**moving average in the statistics literature**

![image-20211111135406374](../../pictures/DL6-3-2.png)

## 6.4 understanding exponentially weighted averages

![image-20211111140352788](../../pictures/DL6-4-1.png)

![image-20211111140656770](../../pictures/DL6-4-2.png)

## 6.5 Bias correction in exponentially weighted average

![image-20211111141211960](../../pictures/DL6-5-1.png)

能够处理初始的偏差

## 6.6 Gradient descent with momentum(动量)

**Basic idea: ** to compute an exponentially weighted average of your gradients, and then use that gradient to update your weights instead.

用于加速梯度下降

**diverging: 不同**

减缓了梯度下降的速度,使得在横轴的方向上走的更远。

![image-20211111142645797](../../pictures/DL6-6-1.png)

**robust: 健壮性 **  **omitted: 省略了**

![image-20211111143113189](../../pictures/DL6-6-2.png)

## 6.7 RMSprop（Root mean square prop）

**square root : 平方根**

![image-20211111144431795](../../pictures/DL6-7-1.png)



## 6.8 Adam optimization algrotihm

![image-20211111145119424](../../pictures/DL6-8-1.png)

**adaptive: 自适应**

Adam: Adaptive Moment Estimation

![image-20211111145538583](../../pictures/DL6-8-2.png)



## 6.9 Learning rate decay (衰减)

Recall that one epoch is one pass through the data.

![image-20211111150100210](../../pictures/DL6-9-1.png)

**discrete: 离散**

![image-20211111150703212](../../pictures/DL6-9-2.png)

## 6-10  The problem of local optima 

**saddle points : 鞍点**

![image-20211111151752047](../../pictures/DL6-10-1.png)

![image-20211111152052458](../../pictures/DL6-10-2.png)







































