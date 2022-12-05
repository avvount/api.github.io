---
title: VBox从U盘启动
mathjax: false
date: 2018-02-28 13:10:59
tags:
    - Linux
    - VBox
---

在U盘上装了个arch，想使用VBox从U盘启动，在网上找到了方法，其实不仅仅是U盘，可以是任何一块硬盘。方法记录在这里

# 使用VBox的用户需要加入vboxusers组(宿主机)  

# 更改权限  

用户需要对要使用的U盘设备文件有读写权限  

`sudo chmod o+rw /dev/sdx`

# 创建VMDK文件  

在帮助VBox帮助文档上找到以下内容  

> To create an image that represents an entire physical hard disk (which will not contain any actual data, as this will all be stored on the physical disk), on a Linux host, use the command  
`VBoxManage internalcommands createrawvmdk -filename /path/to/file.vmdk -rawdisk /dev/sdx`  

执行上边这条命令后，使虚拟机从刚刚创建到vmdk文件启动即可


* 每次想从U盘启动时都要先执行一次第二步

# 从硬盘的指定分区启动  

帮助文档如下：
>To create a special image for raw partition support (which will contain a small amount of data, as already mentioned), on a Linux host, use the command
`VBoxManage internalcommands createrawvmdk -filename /path/to/file.vmdk
-rawdisk /dev/sda -partitions 1,5`  
As you can see, the command is identical to the one for “full hard disk” access, except for the additional -partitions parameter. This example would create the image /path/to/file.vmdk (which, again, must be absolute), and partitions 1 and 5 of /dev/sda would be made accessible to the guest.


  
