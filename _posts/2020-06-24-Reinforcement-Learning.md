---
layout: post
title: "百度强化学习7日打卡营学习笔记"
author: "sush"
header-img: "img/post-bg-web.jpg"
header-mask: 0.4
tags:
  - machine learning
---
### **百度7日强化学习训练营学习笔记**
一直都对强化学习很感兴趣，之前通过莫凡python对强化学习有了一个大致印象，但是不太深入。这次通过百度强化学习7日训练营，跟随科科老师相对系统的学习了强化学习的基础知识、常用模型以及模型应用的场景。下面通过笔记的方式记录这7天所学的内容。  

#### 什么是强化学习
智能体agent在环境environment中学习，根据环境的状态state（或观测到的observation），执行动作action，并根据环境的反馈 reward（奖励）来指导更好的动作。  
*注意：从环境中获取的状态，有时候叫state，有时候叫observation,一个代表全局状态，一个代表局部观测值。在多智能体环境会有差别，对于单智能体等价。*  
强化学习的基本要素：  
<img src="/blog/img/in-post/reforce_1.png">
agent会和enviroment进行交互(action),从而改变enviroment的state,并获得reward(奖励或者惩罚)
<img src="/blog/img/in-post/reforce_learning.png">
强化学习与监督学习有很相似的地方，监督学习通过标签进行学习，强化学习通过reward进行优化；不同之处在于监督学习主要用来认知问题，而强化学习用来做出决策，另外强化学习善于处理长期reward的问题。  
用一张科科老师的PPT总结强化学习基本概念
<img src="/blog/img/in-post/reforce_2.png">






