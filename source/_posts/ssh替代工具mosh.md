---
title: ssh替代工具mosh
mathjax: false
date: 2018-01-24 21:27:45
tags:
    - VPS
    - Linux
---
放假回家，才发现广电宽带跟校园网简直没法比，这次真是见识到了GFW的威力，不到十天，给我封了三四个IP了。ssh连接VPS也老是掉线，甚至连不上去，终于在网上找到一个很棒的工具——mosh，跟ssh类似，同时需要服务端和客户端，使用方法也很像，使用命令`mosh USERNAME@IP`。  
若更改了ssh默认端口，比如改为9559，则命令为`mosh --ssh="ssh -p 2022" USERNAME@IP`  
其他复杂配置没有仔细研究，这些对我来说就足够用了

  
