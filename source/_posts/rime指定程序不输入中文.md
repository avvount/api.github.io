---
title: rime指定程序不输入中文
mathjax: false
date: 2018-04-05 21:14:13
tags:
    - Windows
---
如在winkawaks.exe中不输入中文则如此设定：  
>## squirrel.custom.yaml  
```yaml
patch:  
    app_options/winkawaks.exe:  
        ascii_mode: true  
```
  
