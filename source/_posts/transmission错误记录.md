---
title: transmission错误记录
mathjax: false
date: 2018-01-24 20:45:22
tags:
    - transmission 
    - VPS 
    - Linux
---
在VPS上使用transmission-daemon时出现以下错误
```
UDP Failed to set receive buffer: requested 4194304, got 425984 (tr-udp.c:84) 
UDP Failed to set send buffer: requested 1048576, got 425984 (tr-udp.c:95) 
```
这是UDP缓存区不足引起的，可调大UDP缓冲区解决
```
sysctl -w net.core.rmem_max=4195328 
sysctl -w net.core.wmem_max=4195328
```
执行以上命令，并写入/etc/sysctl.conf中

  
