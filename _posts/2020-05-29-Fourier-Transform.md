---
layout: post
title: "第一篇博客 傅里叶变换理解"
author: "sush"
header-img: "img/post-bg-web.jpg"
header-mask: 0.4
tags:
  - Fourier Transform
---
### **傅里叶变换及其理解**
#### **动机** ####
这是本人在github上的第一篇博客，之所以写博客一是想把自己的学习和思考过程记录下来，二是想加深自己对技术的理解。
就像第一篇博客傅里叶变换，本科是一名电子狗，大学期间就系统的学习过信号系统的课程，为了应付考试还背过常用傅里叶变换的公式。然而当时就不甚理解，自己也没有深入思考，早就把本来不多的所学抛到九霄云外。如今成为一名算法工程师，没想到和这个老朋友又见面了，所以这次想把他搞清楚。

#### “任何”周期信号都可以用一系列成谐波关系的正弦曲线来表示 ####
<img src="http://latex.codecogs.com/gif.latex? f(t)=c_0+\sum_{n=1}^{\infty}c_n\cos(n{\omega}t+{\phi})">
<center>傅里叶级数</center>
<img src="http://latex.codecogs.com/gif.latex? f(t)=c_0+\sum_{n=1}^{\infty}[c_n\cos\phi \cos(n\omega t)-c_n\sin\phi sin(n\omega t)]">
以下为检波和求解系数的过程：
<img src="http://latex.codecogs.com/gif.latex?f(t)=c_0+\sum_{n=1}^{\infty}[a_n\cos(n\omega t)+b_n\sin(n\omega t)]">
<img src="http://latex.codecogs.com/gif.latex?\int_0^Tf(t)\sin(n\omega t)dt=b_n\int_0^T\sin(n\omega t)\sin(k\omega t)dt=b_n\int_0^T\sin(n\omega t)^2dt">
<img src="http://latex.codecogs.com/gif.latex?\int_0^Tf(t)\sin(n\omega t)dt=b_n\frac{T}{2}">
b_n=\frac{2}{T}\int_0^Tf(t)\sin(n\omega t)dt
解释：由于三角函数的正交性，不同频率的正余弦波相乘，对其周期积分后，结果为0
同样可求出<img src="http://latex.codecogs.com/gif.latex?\\a_n">,进而求出<img src="http://latex.codecogs.com/gif.latex?\\\phi">
<img src="http://latex.codecogs.com/gif.latex?c_n=\sqrt[2]{a_n^2+b_n^2}">
<img src="http://latex.codecogs.com/gif.latex?\phi=arctan(-\frac{b_n}{a_n})">

#### "傅里叶级数用于对周期信号转换，傅里叶变换用于对非周期信号转换" ####
<img src="http://latex.codecogs.com/gif.latex?F(f(t))=\int_{-\infty}^{\infty} f(t)e^{-i\omega t} dt">
根据欧拉公式：
<img src="http://latex.codecogs.com/gif.latex?e^{i\theta}=\cos\theta+i\sin\theta">
带入可得：
<img src="http://latex.codecogs.com/gif.latex?F(f(t))=\int_{-\infty}^{\infty}f(t)[\cos(\omega t)-i\sin(\omega t)]dt">
<img src="http://latex.codecogs.com/gif.latex?F(f(t))=\int_{-\infty}^{\infty}f(t)\cos(\omega t)dt-\int_{-\infty}^{\infty}f(t)i\sin(\omega t)dt">
和傅里叶级数相比，无非就是多了个复数，积分区间从负无穷到正无穷

#### "傅里叶变换要求时域信号绝对可积，对于不满足绝对可积条件的连续信号采用拉普拉斯变换" ####
<img src="http://latex.codecogs.com/gif.latex?F(s)=\int_{-\infty}{\infty}f(t)e^{-st}dt=\int_{-\infty}^{\infty}e^{(-\sigma+i\omega t)}dt">
所以拉普拉斯与连续时间的傅里叶变换的关系是:
##### 拉普拉斯变换将频率从实数推广为复数，傅里叶变换是拉普拉斯变换的一个特例（当s为纯虚数时，f(t)的拉普拉斯变换等同于傅里叶变换） #####

#### 离散信号傅里叶变换和Z变换 ####
<img src="http://latex.codecogs.com/gif.latex?\sum_{-\infty}^{\infty}x[n]e^{-j\omega n}">
<center>DTFT</center>

<img src="http://latex.codecogs.com/gif.latex?\sum_{-\infty}^{\infty}x[n]z^{-n}">
<img src="http://latex.codecogs.com/gif.latex?z=(a*e^{jw})^{-n}">
<center>Z变换</center>
对应连续时间的傅里叶变换和拉普拉斯变换
从图像的角度来说，Z变换得到的频谱，是一个复平面上的函数，而DTFT得到的频谱，则是沿着单位圆切一刀，得到的函数的剖面，从负实轴切断展开的图像。