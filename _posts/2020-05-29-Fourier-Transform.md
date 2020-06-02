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
同样可求出<img src="http://latex.codecogs.com/gif.latex?a_n">,进而求出<img src="http://latex.codecogs.com/gif.latex?\phi">
<img src="http://latex.codecogs.com/gif.latex?c_n=\sqrt[2]{a_n^2+b_n^2}">
<img src="http://latex.codecogs.com/gif.latex?\phi=arctan(-\frac{b_n}{a_n})">

#### "傅里叶级数用于对周期信号转换，傅里叶变换用于对非周期信号转换" ####
<img src="http://latex.codecogs.com/gif.latex?F(f(t))=int_-infty^infty f(t)e^-i\omega t \delta t">