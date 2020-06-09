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
<img src="/blog/img/in-post/">

#### Graph指用顶点和边建立相应关系的拓扑结构 ####
度矩阵D是一个对角矩阵，对角线上元素依次为各个顶点的度  
邻接矩阵A描述的是各个顶点和其他顶点边存在的情况
<img src="/blog/img/in-post/laplacian_matrix.png">

#### 三种拉普拉斯矩阵 ####
<center>Combinatorial Laplacian</center>
<img src="http://latex.codecogs.com/gif.latex? L=D-A">
<img src="/blog/img/in-post/combinatorial_laplacian.png">


<center>Symmetric normalized Laplacian</center>
<img src="http://latex.codecogs.com/gif.latex? L^{sym}=D^{-\frac{1}{2}}">
<img src="/blog/img/in-post/sym.png">

<center>Random walk normalized Laplacian</center>
<img src="http://latex.codecogs.com/gif.latex? L^{sym}=D^{-\frac{1}{2}}LD^{-\frac{1}{2}}=I-D^{-\frac{1}{2}}AD^{-\frac{1}{2}}">
<img src="/blog/img/in-post/rwnl.png">

##### 拉普拉斯矩阵性质 #####
(1)拉普拉斯矩阵是对称矩阵，可以进行特征分解(谱分解)
(2)拉普拉斯矩阵只在中心顶点和一阶相连的顶点上（1-hop neighbor）有非0元素，其余之处均为0

#### 拉普拉斯矩阵谱分解(特征分解) ####
由于拉普拉斯矩阵是实对称矩阵，有以下性质:  
1 对称矩阵一定n个线性无关的特征向量  
2 特征值一定非负  
3 对称矩阵特征向量相互正交  

由于1性质，拉普拉斯矩阵可以进行特征分解（谱分解）
<img src="/blog/img/in-post/spectral_domain.png">

#### 图上的傅里叶变换 ####
图神经网络的核心工作是对空间域(Spatial Domain)中节点的Embedding进行卷积操作(即聚合邻居Embedding信息)，然而图数据和图像数据的差别在于节点邻居个数、次序都是不定的，因此传统用于图像上的CNN模型中的卷积操作(Convolution Operator)不能直接用在图上，因此需要从频谱域(Spectral Domain)上重新定义这样的卷积操作再通过卷积定理转换回空间域上。

为了在频谱域和空间域中转换，我们借助了傅里叶公式，并且定义了图上傅里叶变换(从空间域变换到频谱域)和图上傅里叶逆变换(从频谱域回到空间域)的变换公式。具体操作是我们将节点的Embedding通过傅里叶正变换从空间域变换到了频谱域
，在频谱域上和卷积核进行卷积操作，再将变换后的节点Embedding通过傅里叶逆变换回到空间域，参与后续的分类等任务。  

详情还是参见这篇博客吧，写的很具体
[GNN 教程：漫谈谱图理论和GCN的起源](https://archwalker.github.io/blog/2019/06/16/GNN-Spectral-Graph.html)




