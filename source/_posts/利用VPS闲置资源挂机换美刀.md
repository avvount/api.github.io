---
title: 利用VPS闲置资源挂机换美刀
mathjax: false
date: 2018-02-26 11:29:12
tags:
    - VPS
    - Linux
---

挂机需安装vncserver、一个轻量级桌面以及firefox，在debian9下我安装的是tightvncserver、openbox和firefox-esr。

# 挂ebesucher  
有两种方式
1. 安装firefox<54版本，安装[ebesucher扩展](https://www.ebesucher.com/data/firefoxaddon/latest.xpi )进行挂机
2. 打开挂机页面 `https://www.ebesucher.com/surfbar/USERNAME` 进行挂机,可设置该页面为主页

# 挂Vagex

下载firefox [Vagex](https://addons.mozilla.org/en-US/firefox/addon/vagex2/)扩展，设置扩展跟随浏览器启动进行挂机

# 更好的挂机  

## 设置定时任务  
由于VPS配置较低，浏览器可能崩溃，可设置定时任务定时重启vncserver，并设置firefox跟随openbox自启动

## 对firefox进行配置  

1. 设置浏览器不保存历史记录  
2. 设置浏览器不保存cookies  
    - 打开about:config 
    - 搜索 browser.privatebrowsing.autostart  設定為true 


  
