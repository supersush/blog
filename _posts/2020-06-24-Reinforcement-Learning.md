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
注意：从环境中获取的状态，有时候叫state，有时候叫observation,一个代表全局状态，一个代表局部观测值。在多智能体环境会有差别，对于单智能体等价。  
<img src="/blog/img/in-post/reforce_learning.png">



