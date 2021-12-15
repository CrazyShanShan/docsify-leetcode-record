# 12. Support Vector Machines

## 12.1 Optimization objective(优化目标）

![image-20211104102831211](../../pictures/ML12-1.1.png)

![image-20211104103534183](../../pictures/ML12-1.2.png)

![image-20211104103652627](../../pictures/ML12-1.3.png)

## 12.2 Large Margin(最大间隔) Intuition  ![image-20211104104152414](../../pictures/ML12-2.1.png)

![image-20211104104746435](../../pictures/ML12-2.2.png)

![image-20211104104954447](../../pictures/ML12-2.3.png)

![image-20211104105358561](../../pictures/ML12-2.4.png)

## 12.3 The mathematics begind large margin classification(optional) 

**projection： 投影** **derivation: 推导**

![image-20211104110325378](../../pictures/ML12-3.1.png)

![image-20211104111025624](../../pictures/ML12-3.2.png)

## 12.4 Kernels 1

![image-20211104114314352](../../pictures/ML12-4.1.png) ![image-20211104114702895](../../pictures/ML12-4.2.png)

 ![image-20211104115034120](../../pictures/ML12-4.3.png)

![image-20211104115428256](../../pictures/ML12-4.4.png)

![image-20211104115959409](../../pictures/ML12-4.5.png)

## 12.5 Kernels 2

![image-20211104140710412](../../pictures/ML12-5.1.png)

![image-20211104141643726](../../pictures/ML12-5.2.png)

 ![image-20211104142024697](../../pictures/ML12-5.3.png)

## 12.6 Using an SVM

Need to specify:

- Choice of mparameter C
- Choice of kernel(similarty function)

E.g . No kernel ("linear kernel") -> Predict "y =1 " if $\theta^Tx \ge 0$   n large, m smaller

Gaussian kernel n small., m large
$$
f_i = exp\left(-\frac{||x - l^{(i)}||^2}{2\sigma^2}\right), where \ l^{(i)} = x^{(i)}
$$
Need to choose $\sigma^2$

![image-20211104143507801](../../pictures/ML12-6.1.png)

![image-20211104143955405](../../pictures/ML12-6.2.png)

![image-20211104144201485](../../pictures/ML12-6.3.png)

![image-20211104145235515](../../pictures/ML12-6.4.png)











































