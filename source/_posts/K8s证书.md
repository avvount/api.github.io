---
title: K8s 证书更新
date: 2022-12-05 10:15:25
tags: K8s
---
## 证书文件说明  
证书文件均在/etc/kubernetes/pki/下  

### Kubernetes 集群根证书  

`ca.crt ca.key`  
由此根证书签发的证书有:  
  1. kube-apiserver 组件持有的服务端证书  
  `apiserver.crt apiserver.key`
  2. kubelet 组件持有的客户端证书  
  `apiserver-kubelet-client.crt apiserver-kubelet-client.key`

* 注意  
kubelet 上一般不会明确指定服务端证书, 而是只指定 ca 根证书, 让 kubelet 根据本地主机信息自动生成服务端证书并保存到配置的cert-dir文件夹中。轮换的证书默认位于目录 /var/lib/kubelet/pki。

### 汇聚层(aggregator)证书  

`front-proxy-ca.crt front-proxy-ca.key`

由此根证书签发的证书只有一组:  
  1. 代理端使用的客户端证书, 用作代用户与 kube-apiserver 认证  
    `front-proxy-client.crt front-proxy-client.key`

### etcd 集群根证书  

`etcd/ca.crt etcd/ca.key`

由此根证书签发机构签发的证书有:  
  1. etcd server 持有的服务端证书  
    `etcd/server.crt etcd/server.key`  
  2. peer 集群中节点互相通信使用的客户端证书  
    `etcd/peer.crt etcd/peer.key`  
  3. pod 中定义 Liveness 探针使用的客户端证书  
    `etcd/healthcheck-client.crt etcd/healthcheck-client.key`  
  4. 配置在 kube-apiserver 中用来与 etcd server 做双向认证的客户端证书  
    `apiserver-etcd-client.crt apiserver-etcd-client.key`  
    
### Serveice Account秘钥  

`sa.crt sa.key`  

这组的密钥对仅提供给 kube-controller-manager 使用。 kube-controller-manager 通过 sa.key 对 token 进行签名, master 节点通过公钥 sa.pub 进行签名的验证.

以下几种证书在所有master节点的都一样，证书有效期为10年
├── ca.crt  
├── ca.key  
├── sa.key  
├── sa.pub  
├── front-proxy-ca.crt  
├── front-proxy-ca.key  
├── etcd  
├── ├── ca.crt  
├── ├── ca.key  

以下证书每次更新时需要在每个master节点进行更新，证书默认有效期为1年 
├── apiserver.crt  
├── apiserver.key  
├── apiserver-kubelet-client.crt 
├── apiserver-kubelet-client.key
├── front-proxy-client.crt 
├── front-proxy-client.key
├── apiserver-etcd-client.crt  
├── apiserver-etcd-client.key
├── etcd  
├── ├── healthcheck-client.crt  
├── ├── healthcheck-client.key 
├── ├── peer.crt  
├── ├── peer.key 
├── ├── server.crt  
├── ├── server.key 
 
## 证书更新   

以下操作需要在所有master节点执行  

### 生成集群配置的yaml文件
```sh
kubeadm config view > /root/kubeadm.yaml
```  

### 备份数据  

```sh
tar -czvf /etc/kubernetes/ etc-kubernetes.tar.gz
tar -czvf /var/lib/etcd etcd.tar.gz
```

### 更新证书  
```sh
kubeadm certs renew all --config=/root/kubeadm.yaml
```  

### 更新conf配置  

1. 删除旧配置文件  

```sh
rm /etc/kubernetes/admin.conf /etc/kubernetes/kubelet.conf /etc/kubernetes/controller-manager.conf /etc/kubernetes/scheduler.conf 
```

2. 生成新配置文件   

```sh
kubeadm init phase kubeconfig all --config /root/kubeadm.yaml
```

3. 更新kubeconfig文件  

```sh
cp $HOME/.kube/config $HOME/.kube/config.old
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
chown $(id -u):$(id -g) $HOME/.kube/config
```

### 检查证书到期时间是否延长  
```sh
kubeadm certs check-expiration  
```


### 重启 kube-apiserver kube-controller-manager kube-scheduler etcd  

```sh
systemctl restart kublet
# docker ps | grep -E 'k8s_kube-apiserver|k8s_kube-controller-manager|k8s_kube-scheduler|k8s_etcd_etcd' | awk -F ' ' '{print $1}' | xargs docker restart
```


[PKI证书和要求](https://kubernetes.io/zh-cn/docs/setup/best-practices/certificates/)  
[使用 kubeadm 进行证书管理](https://kubernetes.io/zh-cn/docs/tasks/administer-cluster/kubeadm/kubeadm-certs/)  
[使用 kubeadm 进行证书管理 - 博客园](https://www.cnblogs.com/zhangrui153169/p/15814148.html)
