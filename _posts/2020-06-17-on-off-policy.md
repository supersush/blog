---
layout: post
title: "强化学习中的重要概念"
author: "sush"
header-img: "img/post-bg-web.jpg"
header-mask: 0.4
tags:
  - Math
---
### **强化学习中几个重要概念**
### On Policy(SaSa) VS Off Policy(Q learning) 
on-policy与off-policy的本质区别在于：
更新Q值(价值函数)时使用的方法是沿用既定策略(on-policy)还是使用新策略(off-policy)  
其中更新Q值得策略称为评估策略；采取动作的策略称为行动策略。换而言之，评估策略和行动策略是一个策略则称为on policy；不是一个策略则称为off policy
<img src="/blog/img/in-post/on_off_policy.png">  

### Value based VS Policy based
Values based模型需要Q值函数判断出每个动作的价值，然后根据价值函数做出行为决策（action选择）  
Policy based模型直接根据当前状态直接做出行为决策（点估计（直接输出action）或概率估计（输出action概率值）)  

In Policy-based methods we explicitly build a representation of a policy (mapping π:s→a) and keep it in memory during learning. In Value-based we don't store any explicit policy, only a value function. The policy is here implicit and can be derived directly from the value function (pick the action with the best value)

### Deterministic VS NON-Deterministic
确定性策略指的是相同state下，action的选择是确定的
非确定性策略值得是相同state下，action的选择是依据一定概率分布的（非确定的）

The algorithms in which the result of every algorithm is uniquely defined are known as the Deterministic Algorithm. ... On other hand, the algorithms in which the result of every algorithm is not uniquely defined and result could be random are known as the Non-Deterministic Algorithm.  

确定性策略没有探索性怎么办？  
为了学习过程可以增加一些随机性，增加学习的覆盖，确定性策略对选择出来的动作𝐴会增加一定的噪声N，最终选择的Action=u(s)+N

注意：确定性策略和非确定性策略指的是策略梯度更新的方式（训练阶段）；在预测阶段都是确定性的（概率最大的值或者直接输出的值）  

### PG和DPG的区别
其实就是确定性策略和非确定性策略的区别，这里需要重点关注两者的策略梯度更新公式（策略由行为策略和评估策略共同组成）    
<img src="/blog/img/in-post/SPG_VS_DPG.png">  

### 强化学习和监督学习的区别
1.监督学习偏学习，强化学习偏决策  
2.监督学习更像是评估策略，强化学习既有评估策略也有行动策略（具有更强的探索性）
