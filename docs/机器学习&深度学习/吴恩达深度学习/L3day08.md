# 8 Introduction to ML stategy

## 8.1 Why ML Strategy?

Ideas:
1. Collect more data
2. Collect more diverse training set
3. train algorithm longer with gradient descent
4. try adam instead of gradient descent
5. try bigger network
6. try smaller network
7. try dropout
8. add l2 regularization
9. network architecture
		1. activation functions
		2. hidden units

## 8.2 Orthogonalization(正交化)

其实就是一次改变一个变量, 这里是从不同的维度的

Chain of assumptions in ML:

1. Fit training set well on cost function 
	1. bigger network
	2. adam
2. Fit dev set well on cost function 
	1. regularization
	2. bigger traning set
3. Fit test set well on cost function
	1. bigger dev set
4. Performs well in real world
	1. change dev set or cost function


## 8.3 Single number evaluation metirc(指标)

have s gingle number evaluation metric can really help 


## 8.4 Satisficing and optimizing metrics

N metrics you need to care about, it's sometimes reasonable to pick one of them to be optimizing.

So you want to do as well as is possible on that one. Others should be set as satisficing.

## 8.5 Train/dev/test distributions 

take all this data, randomly shuffled data into the dev and test set.

Guideline:
Choose a dev set and test set to reflect data you expect to get in the future and consider important to do well on.


## 8.6 Size of dev and test sets

Old way of splitting data:
1. 0.7 train 0.3 test
2. 0.6 train 0.2 dev 0.2 test

size of test set: 0.05
set your test set to be big enough to give high confidence in the overall performance of your system

## 8.7 When to change dev/test sets and metrics


exp: 
Metirc: classification error
Algorithm A: 3% error but includes porn
Algorithm B : 5% error 

Error: 
$$
\frac{1}{\sum_{i}{w^i}} \sum_{i = 1}^{m_{dev}}w^{(i)} L(y_{pred}^{(i)} != y^{(i)})
$$

其中$w^i$ 为惩罚权重，如果这个$x^{i}$是色情图片，就给予一个更高的权重, 因此这里需要你去给train和dev手动去标记哪些是色情图片

Orthogonalization for cat pictures: anti-porn

1. So far we've only discussed how to define a metric to evaluate classifiers.
2. Worry separately about how to do well on this metric.

Another example 

A: 3% error 

B: 5% error 

If doing well on your metric  + dev/test set does not correspond to doing well on your application, change your metric and/or dev/test set.



## 8.8 Why human-level performance?

Why compare to human-level prrformance 

Humans are quite good at a lot of tasks. SO long as ML is worse than humans, you can:

- Get labeled data from humans.

- Gain insight from manual error analysis:

  Why did a person get this right?

- Better analysis of bias/variance.

  

## 8.9 Avoidable bias

Focus on bias or variance is depended on Humans  

Avoid bias is between Humans and training error.

Variance is between traning error and dev 



## 8.10 Understanding human-level performance

compare available bias and variance



## 8.11 Surpassing human-level performance

略



## 8.12 Imporving your model performance

Avoidable bias :

1. train bigger model
2. train longer/better optimization algorithms
3. NN architecture/hyperparameters search 

Variance: 

1. More data
2. Regularazation
   1. L2, dropout, data augmentation
3. NN architecture/hyperparameters search





























































































