---
title: 保持ssh连接
mathjax: false
date: 2018-02-27 08:41:14
tags:
    - Linux
    - VPS
---

使用ssh连接远程服务器经常被强行中断，使用mosh可以避免这一问题，但mosh无法向上翻页，还是想使用ssh，在网上找到了些解决办法。在此记录其中两种。

# 配置服务端  

在服务端配置文件 `/etc/ssh/sshd_config` 中添加以下内容

```
ClientAliveInterval 30  
ClientAliveCountMax 60
```
第二行配置表示如果发送 keep-alive 包数量达到 60 次，客户端依然没有反应，则服务端 sshd 断开连接。如果什么都不操作，该配置可以让连接保持 30s*60=30 min.  
配置完成后重启sshd

# 配置客户端  

还可以通过客户端配置实现，在客户端配置文件`/etc/ssh/ssh_config`中添加以下内容  
```
ServerAliveInterval 30  
ServerAliveCountMax 60  
```
本地 ssh 每隔30s向 server 端 sshd 发送 keep-alive 包，如果发送 60 次，server 无回应断开连接。


  
