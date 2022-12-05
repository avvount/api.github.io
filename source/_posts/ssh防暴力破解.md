---
title: ssh防暴力破解
date: 2018-01-14 15:45:30
tags:
    - VPS 
    - Linux
---
  
## 查看多次登录失败IP
```
# grep "Failed password for root" /var/log/auth.log | awk '{print $11}' | sort | uniq -c | sort -nr | grep -v ";"  
lastb | awk '{ print $3}' | sort | uniq -c | sort -n
```  

## 更改ssh端口  

## 设置强密码  

## 使用denyhosts

  
  
