# 11. Case Studies

## 11.1 Why look at case studies? 

- LetNet-5
- AlexNet
- VGG 
- ResNet
- Inception

## 11.2 Classic networks

![image-20211123192309724](../../pictures/DL11-2-1.png)

- LeNet: Paramters: 60,000 

- AlexNet: 60,000,000
  - ReLU
  - Mutilpe GPS
  - LRN: this doesn't make sense
- VGG - 16: 138,000,000

![image-20211123193308283](../../pictures/DL-11-2-2.png)

![image-20211123194050116](../../pictures/DL11-2-3.png)

## 11.3 Residual Networks(ResNets)

We'll learn skip connection which allows you to take the activation from one layer and suddenly feed it to another layer, even much deeper in the neural network. And using that, you're going to build ResNets which enables you to rain very very deep networks, sometimes even networks of over 100 layers.

ResNets are built out of something called a residual block.

just add a a l before applying to nonlinearity, the ReLU nonlinearity.

![image-20211123194938967](../../pictures/DL11-3-1.png)

![image-20211123195313351](../../pictures/DL11-3-2.png)

## 11.4 Why ResNets work

![image-20211123200218253](../../pictures/DL11-4-1.png)

![image-20211123200615824](../../pictures/DL11-4-2.png)

## 11.5 Network in Network and 1 X 1 convolutions

![image-20211123201902899](../../pictures/DL11-5-1.png)

![image-20211123202231646](../../pictures/DL11-5-2.png)

压缩或者保持或者增加信道数量。

## 11.6 Inception network motivation

What's the inception network or what an inception layer syas is,  is instead of choosing what filter size you want in a CONV layer or even do you want a convolutional layer or pooling layer.

![image-20211123203009100](../../pictures/DL11-6-1.png)

![image-20211123203835672](../../pictures/DL11-6-2.png)

![image-20211123204312619](../../pictures/DL11-6-3.png)

## 11.7 Inception network

![image-20211123205406634](../../pictures/DL11-7-1.png)

## 11.8 Using open-source implementations

略

## 11.9 Transfer learning 

![image-20211123211142188](../../pictures/DL11-9-1.png)

## 11.10 Data augmentation

Mirroring , Random 

PCA COlor 

![image-20211123212039654](../../pictures/DL11-10-1.png)

## 11.11 The state of computer vision 

提高基准的方法： Multi-crop ，10-crop，一个图片取10个地方的偏移，正中心+左上右下右上左下+image+左上右下右上左下 = 10 ,然后再来去预测

Use open source code 

- Use architectures of networks published in the literature 
- Use open source implementations if possible 
- Use pretrained models and fine-tune on your dataset





























 























































