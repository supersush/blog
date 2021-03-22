---
layout: post
title: "python知识点积累"
author: "sush"
header-img: "img/post-bg-web.jpg"
header-mask: 0.4
tags:
  - methond solution
---

#### python包路径相关问题
1.脚本执行，脚本所在目录为环境变量;模块执行，当前目录为环境变量；  
2.相对引用和绝对引用  
from .abc import …是相对引用（开头带点的），一个点指当前目录找，两个点上一级目录，以此类推；  
from abc import … 是绝对引用（正常开头的），系统设定的包搜寻目录里找；  
import abc 永远是绝对引用；  
import .abc 是不允许的；  
