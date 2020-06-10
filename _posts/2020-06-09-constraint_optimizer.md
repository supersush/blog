---
layout: post
title: "带约束凸优化问题"
author: "sush"
header-img: "img/post-bg-web.jpg"
header-mask: 0.4
tags:
  - GCN
---
### **带约束凸优化**
#### **前言** ####
KKT条件是带约束优化存在最优解的必要条件，然而如果简单把带约束最优化问题转换为一个无约束方程组求解，并检验是否满足KKT条件无疑是不现实的；  
对于不等式约束凸优化问题，常用以下两种方式进行迭代求解：  
1.传统的不等式约束优化算法内点法等；  
2.投影梯度下降（约束优化表示下），gt是subgradient,直观含义是每部迭代后，迭代结果可能位于约束集合之外，然后取该迭代结果在约束凸集合上的投影作为新的迭代结果（第二个公式中那个符号标识向X的投影）：  
<img src="/blog/img/in-post/projection.png">

#### 内点法 ####
[主要内容参考这篇文章](https://zhuanlan.zhihu.com/p/32685234)  
线性划归问题一般形式为：  
<img src="/blog/img/in-post/linear-programming.png">
带约束的优化问题我们求解比较麻烦（按无约束求解，检验是否符合约束条件，不符合约束条件解在临界点上），并且难以把求解的过程用代码表示。  
所以将带约束的问题转化为无约束的问题，并且能够用已有的优化算法来求解变成了我们研究的方向（思路类似以前数学老师的口头禅：这个问题你没见过，相似的问题有没有见过，能不能把这个问题转化为以前见过的相似的问题）
##### 线性规划问题的等价（近似）表达 #####
<img src="http://latex.codecogs.com/gif.latex? f(x)=c^{T}x+\sum_{i=1}^{m} I(A_{ij}x_j-b_j)">
其中indicator函数I定义为：
<img src="http://latex.codecogs.com/gif.latex? I(u)=\begin{cases} 0 & \text{if } u \le 0 \\ \infty & \text{if } u > 0 \end{cases}">  
用一个光滑函数代替这个indicator函数：
<img src="http://latex.codecogs.com/gif.latex? I(u)=-\frac{1}{t} log(-u)">
目标函数可写为：  
<img src="http://latex.codecogs.com/gif.latex? f(x)=tc^T x-\sum_{i=1}^m log(-A_{ij} x_j+b_i)">
线性函数是凸函数，I(u)也是凸函数，所以f(x)是凸函数，所以很容易用凸优化经典方法得到该函数的极小值

##### 求解最小值 #####
对于凸函数，函数的极小值为梯度为0时对应的接x*
函数的梯度为：  
<img src="http://latex.codecogs.com/gif.latex? \frac{\partial f}{\partial x_k}=tc_k+\sum_{i=1}^{m}\frac{-A_{ik}}{A_{ij}x_j-b_i">
Hessian矩阵为
<img src="http://latex.codecogs.com/gif.latex? \frac{\partial^2 f}{\partial x_k \partial x_l}=\sum_{i=1}^{m}\frac{A_{ik} A_{il}}{({A_{ij}x_j-b_i})^2}">
定义对角矩阵为  
<img src="http://latex.codecogs.com/gif.latex? D_{ij}=\delta\frac{1}{(A_ik x_k-b_i)^2}">
于是Hessian矩阵写作：
<img src="http://latex.codecogs.com/gif.latex? H_f=A^T D A">
D是正定矩阵，所以Hessian矩阵至少半正定，所以f(x)是凸函数。  
因为D为可逆矩阵，矩阵A满秩，所以Hessian矩阵可逆（线性代数基础还是很重要），所以要计算\nabla f=0 的根，可以用牛顿迭代法  

牛顿迭代法：  
<img src="http://latex.codecogs.com/gif.latex? x^{(n+1)}=x^{(n)}-H^{-1}\nabla f">
参数t固定，对于每一个t都可以得到一个解x_t;其中最大的t对应的解最精确





