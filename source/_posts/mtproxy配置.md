---
title: mtproxy配置
date: 2021-06-19 16:30:05
tags:
---

1. 获取 Telegram ipv4 服务器列表及配置
```sh
curl -s https://core.telegram.org/getProxyConfig -o proxy-multi.conf
```


2. 获取 Telegram ipv6 服务器列表及配置
```sh
curl -s https://core.telegram.org/getProxyConfigV6 -o proxy-multi.conf
```

3. MTProxy.service
```ini
[Unit]
Description=MTProxy
After=network.target

[Service]
Type=simple
WorkingDirectory=/etc/mtproxy
ExecStart=/usr/local/bin/mtproto-proxy -u nobody -p 8888 -H 6443 -S <secret> -P <proxy tag> --aes-pwd proxy-secret proxy-multi.conf -M 1 --address 127.0.0.1
Restart=on-failure

[Install]
WantedBy=multi-user.target

```

4. 其他从网上现查吧