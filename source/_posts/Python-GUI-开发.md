---
title: Python GUI 开发
date: 2021-06-13 16:25:17
tags:
    - Python 
---

之前尝试过使用tkinter写python界面,但是没用过可视化的界面设计工具,今天简单玩儿了一下PyQt和PAGE

## PAGE 
是基于tkinter的,界面有点丑,但貌似比PyQt轻量一些,感觉不太好用
界面拖拽完成后点击Gen_Python->Generate Python GUI和Gen_Python->Generate Support Module,一共生产了三个文件page.tcl、page.py、page_support.py，通过page.py来启动

选定控价点击"Set Command"，弹出窗口中输入回调函数，回调函数会生成在page_support.py里


## PyQt
安装PyQt5和pyqt5-tools两个模块，pyqt5-tools包里带了qt designer。

qt designer的界面就比较友好了，带中文界面，界面拖拽完成后保存，会生成一个.ui文件，执行`pyuic5 - o xxx.py xxx.ui`将ui文件转换为python代码
新建一个python文件，贴入以下代码，Ui_Dialog是designer设计好的对话框控件对象，信号和槽的连接可以在designer中设置也可以在MainDialog类中写，但是在designer里貌似不能自定义槽函数，这种就不得不自己写connect函数了


```py
import sys
from PyQt5.QtWidgets import QApplication, QDialog
from pyqt_demo import Ui_Dialog

class MainDialog(QDialog, Ui_Dialog):
    def __init__(self, parent=None):
        super(QDialog, self).__init__(parent)
        self.setupUi(self)

if __name__ == '__main__':
    myapp = QApplication(sys.argv)
    myDlg = MainDialog()
    myDlg.show()
    sys.exit(myapp.exec_())
```

## 资源  

[各种各样的PyQt测试和例子](https://github.com/PyQt5/PyQt)