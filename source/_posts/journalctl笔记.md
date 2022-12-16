---
title: journalctl笔记
date: 2022-12-16 08:26:31
tags:
    - Linux
---

## 服务配置

```sh
mkdir /var/log/journal
mkdir /etc/systemd/journald.conf.d
cat > /etc/systemd/journald.conf.d/99-prophet.conf <<EOF
[Journal]
# 持久化保存到磁盘
Storage=persistent

#压缩历史日志
Compress=yes

SyncIntervalSec=5m
RateLimitInterval=30s
RatelimitBurst=1000

#最大占用空间10G
SystemMaxUse=10G

#单日志文件最大200M
SystemMaxFileSize=200M

#日志保存时间2周
MaxRetentionSec=2week

#不将日志转发到syslog
ForwardToSyslog=no
EOF

systemctl restart systemd-journald
```

## 清理日志  

只保留最近两天的日志  
```sh
journalctl --vacuum-time=2d
```
只保留最近500MB日志  
```sh
journalctl --vacuum-size=500M
```