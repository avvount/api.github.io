---
title: Kubernetes
date: 2020-04-18 23:32:27
tags: 
    - K8s
    - Linux
---

## 设置rsyslogd和systemd  

见[journalctl笔记](journalctl笔记#服务配置)  

## Docker配置
```sh
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

```sh
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
