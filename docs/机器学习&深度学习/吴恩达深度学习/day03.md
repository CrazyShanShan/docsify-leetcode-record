# 3. One hidden layer Neural Network

## 3.1 Nerual Networks overview

<img src="../../pictures/DL3-1-1.png" alt="image-20211027191726697" style="zoom:50%;" />

## 3.2 Neural Network representation

![image-20211027192340447](../../pictures/DL3-2-1.png)

## 3.3 Computing a neural network's output

<img src="../../pictures/DL3-3-1.png" alt="image-20211027192804726" style="zoom:50%;" />

<img src="../../pictures/DL3-3-2.png" alt="image-20211027193321132" style="zoom:50%;" />

<img src="../../pictures/DL3-3-3.png" alt="image-20211027193706496" style="zoom:50%;" />

W [1] = (4, 3) 4: 层的神经元个数.  3: 输入的个数

W[2] = (1, 4) 1: 层的神经元个数. 4: 输入的个数

## 3.4 Vetorizing across multiple example

<img src="../../pictures/DL3-4-1.png" alt="image-20211027194839736" style="zoom:50%;" />

<img src="../../pictures/DL3-4-2.png" alt="image-20211027195430914" style="zoom:50%;" />

hidden units , training examples.

## 3.5 Explanation for vectorized implementation

<img src="../../pictures/DL3-5-1.png" alt="image-20211027201145715" style="zoom:50%;" />

<img src="../../pictures/DL3-5-2.png" alt="image-20211027201344513" style="zoom:50%;" />

## 3.6 Activation functions

<img src="../../pictures/DL3-6-1.png" alt="image-20211027202032555" style="zoom:50%;" />

## 3.7 Why do you need non-linear activation functions?

略

## 3.8 Derivatives of activation functions

```
sigmoid: g'(z) = a * (1 - a)
tanh: g'(z) = 1 - a ^ 2
ReLU: g'(z) = 1 | 0
```

## 3.9 Gradient descent for neural networks

<img src="../../pictures/DL3-9-1.png" alt="image-20211027203954640" style="zoom:50%;" />

<img src="../../pictures/DL3-9-2.png" alt="image-20211027204529107" style="zoom:50%;" />

## 3.10 Backpropagation intuition(Optional)

<img src="../../pictures/DL3-10-2.png" alt="image-20211027212133399" style="zoom:50%;" />

<img src="../../pictures/DL3-10-3.png" alt="image-20211027212303022" style="zoom:50%;" />

​                                     

```
由上面的推导下面的，麻中麻。
那个a[2] - y是上面算出来的结果。
然后 a[1]T实际上就是x
```

## 3.11 Random Initialization

<img src="../../pictures/DL3-11-1.png" alt="image-20211027213355830" style="zoom:50%;" />

   









