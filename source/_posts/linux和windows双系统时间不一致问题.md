---
title: linux和windows双系统时间不一致问题
mathjax: false
date: 2018-04-05 20:13:54
tags:
    - Linux
---
以下两种方式都可以,推荐第一种方式

##  硬件时钟使用 UTC
参考[archwiki页面](https://wiki.archlinux.org/index.php/Time_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Windows_.E7.B3.BB.E7.BB.9F.E4.BD.BF.E7.94.A8_UTC)  

1.  设置linux使用UTC时间
```zsh
timedatectl set-local-rtc 0 
timedatectl set-ntp 1
```

2. 修改 Windows 注册表  
```bat
Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
```

3. 关闭 Windows 网络对时

## 硬件时钟使用本地时间

1. 设置linux使用本地时间  
```zsh
timedatectl set-local-rtc 1
timedatectl set-ntp 0
```

2. 打开 Windows 网络对时
