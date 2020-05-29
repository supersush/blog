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
$$f(t)=c_0+\sum_{n=1}^{\infty}c_n\cos(n\omega t+\phi)$$
傅里叶级数

$$f(t)=c_0+\sum_{n=1}^{\infty}\[c_n\cos\phi \cos(n\omega t)-c_n\sin\phi sin(n\omega t)\]$$