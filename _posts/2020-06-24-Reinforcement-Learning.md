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
强化学习的单步更新公式：
<img src="/blog/img/in-post/TD_update.png">


#### Q_learning和SARSA
首先我们需要明确什么是on-policy和off-policy<br>
on-policy是指行动策略和评估策略（目标策略）是一个策略。<br>
off-policy是指行动策略和评估策略（目标策略）不是一个策略。这里我们的行动策略是随机策略，以保证充足的探索。评估策略是确定性策略

Q-leaning和SARSA都是基于Q表格进行reward计算和决策的强化学习算法，他们解决的都是状态空间离散且动作空间离散的强化学习问题，不同之处在于两者更新Q表格的方式。

Sarsa全称是state-action-reward-state'-action'，目的是学习特定的state下，特定action的价值Q，最终建立和优化一个Q表格，以state为行，action为列，根据与环境交互得到的reward来更新Q表格。<br>
Sarsa是on-policy的更新方式，先做出动作再更新<br>
<img src="/blog/img/in-post/sarsa_update_function.png">

Q-learning也是采用Q表格的方式存储Q值（状态动作价值），决策部分与Sarsa是一样的，采用ε-greedy方式增加探索。<br>
Q-learning是off-policy的更新方式，更新learn()时无需获取下一步实际做出的动作next_action，并假设下一步动作是取最大Q值的动作。
<img src="/blog/img/in-post/Q-learning-function.png">

#### DQN
对于状态空间有限的决策问题，SARSA和Q-learning还可以解决。当状态空间不可数时，如当面对围棋或机器人控制这类有数不清的状态的环境时，表格型方法在存储和查找效率上都受局限。DQN的提出解决了这一局限，使用神经网络来近似替代Q表格。

本质上DQN还是一个Q-learning算法，更新方式一致。为了更好的探索环境，同样的也采用ε-greedy方法训练。

在Q-learning的基础上，DQN提出了两个技巧使得Q网络的更新迭代更稳定。<br>
1.经验回放 Experience Replay：主要解决样本关联性和利用效率的问题。使用一个经验池存储多条经验s,a,r,s'，再从中随机抽取一批数据送去训练。<br>
2.固定Q目标 Fixed-Q-Target：主要解决算法训练不稳定的问题。复制一个和原来Q网络结构一样的Target Q网络，用于计算Q目标值。

DQN的训练流程：
<img src="/blog/img/in-post/DQN.png">


#### Policy Gradient
在强化学习中，有两大类方法，一种基于值（Value-based），一种基于策略（Policy-based）<br>
&nbsp;Value-based的算法的典型代表为Q-learning和SARSA，将Q函数优化到最优，再根据Q函数取最优策略。<br>
&nbsp;Policy-based的算法的典型代表为Policy Gradient，直接优化策略函数。<br>
策略梯度的求解方式如下：
<img src="/blog/img/in-post/DQN.png">
如果某个策略的reward越大，其梯度乘上的reward越大。类似于监督学习里的正样本权重的概念：正样本（action）权重越大（reward越大），则其预测出现的概率越高（action被选择的概率越高）

另外一点值得说明的是policy gradient算法是随机策略算法。即评估策略（目标策略）是非确定性的。

#### DDPG
之前讲到了对于状态空间连续（不可数），我们采用DQN来扩展Q-learning算法。如果动作空间也连续呢？<br>
DDPG的提出动机其实是为了让DQN可以扩展到连续的动作空间。<br>
&nbsp;DDPG借鉴了DQN的两个技巧：经验回放 和 固定Q网络。<br>
&nbsp;DDPG使用策略网络直接输出确定性动作。<br>
&nbsp;DDPG使用了Actor-Critic的架构

DDPG采用了两个网络：Q网络来学习reward，策略网络来选取action，是一种Actor-Critic架构。通过双网络架构分别解决状态连续和动作连续的问题。
另外DDPG动作空间是连续的，是一种确定性策略算法。

DDPG的结构：
<img src="/blog/img/in-post/DDPG2.png">
<img src="/blog/img/in-post/DDPG.png">

以上便是百度7日强化学习课程的总结，个人感觉强化学习应用的一个难点是模拟器的创建，因为强化学习需要大量和环境的交互才会最终收敛到一个比较好的结果，显然大部分时候不能在真实地场景去交互，所以如何创建仿真环境是应用强化学习要面对的一个问题。











