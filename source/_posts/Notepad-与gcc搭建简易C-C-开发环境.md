---
title: Notepad++与gcc搭建简易C&C++开发环境
date: 2018-04-05 20:01:53
tags:
    - C语言
    - C++ 
    - 编程
---
#  编译
在notepad++中打开“运行”，输入以下代码并保存，可以自定义快捷键以及设置命令名
`cmd /k g++ $(FULL_CURRENT_PATH) -o $(CURRENT_DIRECTORY)\$(NAME_PART) &PAUSE &EXIT`

| cmd /k | 执行命令后不关闭命令窗口 |
|--------|------------------------|
| cmd /c | 执行命令并关闭命令窗口   |
| $(CURRENT_DIRECTORY)|当前所在目录|
| $(FILE_NAME)|当前操作文件的文件名，包含后缀 |
| $(NAME_PART) | 当前操作文件的文件名，不包含后缀|
| $(FULL_CURRENT_PATH)|当前操作文件的完整路径，包括盘符，路径，文件名，后缀  |
| &PAUSE|运行后暂停等待键盘操作 |
| &EXIT|完成后退出运行窗口  |
    
# 执行
输入以下命令并保存：
`cmd /k $(CURRENT_DIRECTORY)\$(NAME_PART) &PAUSE &EXIT`

  
