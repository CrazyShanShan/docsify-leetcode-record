# 5 Setting up your ML application 

## 5. 1  Train/dev/test sets

****

**tuning : 调优**

**training set, dev set , test set**

Prea: 7/3 6/2/2

Big data: 95%/2.5%/2.5%.      99.5%/0.4%/0.1%

**Mismatched train/test distribution:**

```
make sure dev and test comf from same distribution
No having a test set might be okay.(only dev set.)
```

## 5.2 Bias/Variance

![image-20211104204725282](../../pictures/DL5-1-2.png)

  ![image-20211104205353931](../../pictures/DL5-2-2.png)

train set error低， dev set error高： 产生high variance

train set error高，dev set error和train差不多： 产生high bias

在一些高纬数据中，某些部分的数据具有高方差（拟合过度），某些部分的数据具有高偏差（欠拟合）。

## 5.3 Basic "recipe" for machine learning

**basic recipe for machine learning**

**blurry: 模糊的**

```
          Y
high bias -> bigger network, train longer, new network architecture 
(training data performance)
N               
                y
high variance ? -> more data, regulazation, more architecture search
(dev set) 
N 
Done

```

## 5.4 Regularization

---

Logistic regression

![image-20211104211906870](../../pictures/DL5-4-1.png)

---

Neural network

 **arcane: 晦涩难懂**

![image-20211105171718769](../../pictures/DL5-4-2.png)

## 5.5 Why regularization reduce overfitting

![image-20211105172235694](../../pictures/DL5-5-1.png)

![image-20211105172811635](../../pictures/DL5-5-2.png)

## 5.6 Dropout regularization

 ![image-20211105173948403](../../pictures/DL5-6-1.png)

## 5.7 Understanding dropout

Always in dropout.

![image-20211105175341785](../../pictures/DL5-7-1.png)

## 5.8 Other regularization methods

![image-20211106114441333](../../pictures/DL5-8-1.png)

![image-20211106115109447](../../pictures/DL5-8-2.png)

## 5-9 Normalizing(正规化) inputs

1. subtract out or to zero out the mean 
   1. 求平均值
   2. 把每一个数都减去这个平均值，使得新数的平均值为0）
2. normalize the variances（sigma squared is a vector with the variances of each of the features）
   1. 第一步已经计算了每一个x - mean，这里计算$\sigma = \frac {1}{m}\sum_{i = 1}^{m}x^{(i)}**2$   
   2. $x/=\sigma$, 使得x的variance = 1
3. use the same mu and sigma squared to normalize you test set (测试集中做相同的操作需要使用训练集中的平均值和方差值) 

![image-20211106120328456](../../pictures/DL5-9-1.png)

1. By just settin gall of them to a 0 mean and say ,variance 1, thatju st guarantees that all your features on a similar scale and will usually help your learning algorithm run faster.

![image-20211106120934277](../../pictures/DL5-9-2.png)

## 5.10 Vanishing(消失)/exploding(爆炸) gradients

![image-20211106122249257](../../pictures/DL5-10-1.png)

## 5.11 Weight initialization for deep networks

![image-20211107191259145](../../pictures/DL5-11.1.png)

## 5.12 Numerical approximation(数值近视) of gradients 

![image-20211107191848484](../../pictures/DL5-12-1.png)

## 5.13 Gradient Checking

W[1], b[1] 这些由矩阵转换为向量，然后进行连接

![image-20211107192506106](../../pictures/DL5-13-1.png)

![image-20211107192819239](../../pictures/DL5-13-2.png)

 ## 5.14 Gradient Checking implementations

![image-20211107193345139](../../p

ictures/DL5-14-1.png)























