---
title: pm2 & supervisor
date: 2019-08-03 20:24:18
tags:
    - VPS
    - Linux
---

# pm2  
* `pm2 startup`  
    生成pm2-xxx.service

* `pm2 save`   
    保存当前 pm2 运行的各个应用保存到 `~/.pm2/dump.pm2` 下，开机重启时读取该文件中的内容启动相关应用。

# supervisor

