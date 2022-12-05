---
title: Kubernetes
date: 2020-04-18 23:32:27
tags:
---

## 设置rsyslogd和systemd

```shell
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
## Docker配置
```shell
cat > /etc/docker/daemon.json <<EOF
{
    "exec-opts":["native.cgroupdrive=systemd"],
    "log-driver":"json-file",
    "log-opts":{
        "max-size":"100m"
    }
}
EOF
mkdir -p /etc/systemd/system/docker.service.d/
systemctl daemon-reload && systemctl restart docker

```

## 安装Kubeadm

```shell
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=http://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=0
repo_gpgcheck=0
gpgkey=http://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg
    http://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
EOF
```

![内核参数配置](https://github.com/avvount/Picture-Bed/raw/master/K8s%E5%86%85%E6%A0%B8%E5%8F%82%E6%95%B0%E9%85%8D%E7%BD%AE.png)  
![K8s基础镜像](https://github.com/avvount/Picture-Bed/raw/master/k8s%20image.PNG) 
