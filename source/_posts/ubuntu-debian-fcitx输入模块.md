---
title: ubuntu&debian fcitx输入模块
mathjax: false
date: 2018-04-05 20:30:20
tags:
    - Linux
---
1. `fcitx`：fcitx主程序
2. `fcitx-sogoupinyin` ：fcitx的搜狗拼音词库。（你也可以换成其他类型的词库比如五笔、rime等等，具体可以终端输入aptitude search fcitx搜索。）
3. `fcitx-config-gtk`：fcitx的gtk的设置图形界面。
4. `fcitx-frontend-all`：fcitx在所有环境下的前端。（有qt、gtk2、gtk3下对应的包组成。）
5. `fcitx-module-cloudpinyin`：fcitx的云拼音模块。
6. `fcitx-ui-classic`：fcitx的经典UI显示模块。（此软件包不能被fcitx-ui-light或者fcitx-ui-qimpanel代替，因为该包默认包含着fcitx-module-x11，有了它才能在让fcitx在图形界面上显示出输入框。）
7. KDE用户还可以安装fcitx的QT化组件来使fcitx风格能更加与KDE桌面环境统一：`sudo aptitude install fcitx-ui-qimpanel fcitx-module-kimpanel plasma-widget-kimpanel`
s
  
