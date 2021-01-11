---
layout: post
title: "On Policy vs Off Policy"
author: "sush"
header-img: "img/post-bg-web.jpg"
header-mask: 0.4
tags:
  - Math
---
### **强化学习中的On Policy(SaSa)和Off Policy(Q learning)策略**
on-policy与off-policy的本质区别在于：
更新Q值(价值函数)时使用的方法是沿用既定策略(on-policy)还是使用新策略(off-policy)  
其中更新Q值得策略称为评估策略；采取动作的策略称为行动策略。换而言之，评估策略和行动策略是一个策略则称为on policy；不是一个策略则称为off policy
<img src="/blog/img/in-post/on_off_policy.png">



