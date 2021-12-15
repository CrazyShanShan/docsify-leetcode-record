# 7. Hyperparameter tuning 

## 7.1 Tuning process

![image-20211111153012749](../../pictures/DL7-1-1.png)

**denominator: 分母**

![image-20211111153414036](../../pictures/DL7-1-2.png)

 ![image-20211111153618813](../../pictures/DL7-1-3.png)

## 7.2 Using an appropriate scale to pick hyperparameters

**uniformly: 随机均匀**

![image-20211111154227310](../../pictures/DL7-2-1.png)

**logarithmic: 对数** **dedicated: 专用的**

![image-20211111155017387](../../pictures/DL7-2-2.png)

![image-20211111155538211](../../pictures/DL7-2-3.png)

## 7.3 Hyperparameters tuning in practice: Pandas vs. Caviar

 **nudge: 轻推** **caviar: 鱼子酱** **reptiles :爬行动物**

![image-20211111160627915](../../pictures/DL7-3-1.png)

## 7.4 Normalizing activations in a network

![image-20211111161127792](../../pictures/DL7-4-1.png)

![image-20211111161949405](../../pictures/DL7-4-2.png)



## 7.5 Fitting Batch Norm into a neural network

![image-20211112152515682](../../pictures/DL7-5-1.png)

![image-20211112153022384](../../pictures/DL7-5-2.png)

![image-20211112153441042](../../pictures/DL7-5-3.png) 

## 7.6 Why does Batch Norm work?

![image-20211112155150592](../../pictures/DL7-6-1.png)

![image-20211112155725894](../../pictures/DL7-6-2.png)

## 7.7 Batch Norm at test time

 ![image-20211112160707708](../../pictures/DL7-7-1.png)

## 7.8 Softmax regression

![image-20211112161116049](../../pictures/DL7-8-1.png)

![image-20211112161827341](../../pictures/DL7-8-2.png)

![image-20211112162239504](../../pictures/DL7-8-3.png)

## 7.9 Training softmax classifier

![image-20211112162920997](../../pictures/DL8-9-1.png)

you use gradient descent to try to reduce the loss on your training set.

because x for this example is the picture of a cat.

then you want that output probability to be as big as possible.

the cost function really dose is that is looks at whatever is the groud truth class in your training set, and it tries to make the corresponding probablility of that class as high as possible. 

because in that case , the loss will as lower as possible.

![image-20211112164034530](../../pictures/DL7-9-2.png)

![image-20211112164034530](../../pictures/DL7-9-3.png)



## 7.10 Deep Learning frameworks

**less from scratch: 从头开始**

** analogy: 类比** **evolve: 进化** **endorsing: 支持**

**Deep learning frameworks:**
1. Caffe/Caffe2
2. CNTK
3. DL4J
4. Keras
5. Lasagne
6. mxnet
7. PaddlePaddle
8. TensorFlow
9. Theano
10. Torch

## 7.11 TensorFlow
略ICLR



























































































































































