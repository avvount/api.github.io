---
title: rEFInd引导arch
mathjax: false
date: 2018-03-21 15:53:24
tags:
    - Linux
    - Arch
---

使用rEFInd引导系统，配置文件简单，可以自动检测启动项。所以，果断淘汰掉grub2，改用rEFInd。

#  安装

Arch中安装rEFInd安装很简单  
`pacman -S refind-efi`

# 配置  

手动配置Arch Linux菜单，添加菜单项如下  
```
menuentry "Arch Linux" {
    icon     /EFI/refind/refind-theme-regular/icons/128-48/os_arch.png
    loader   /vmlinuz-linux
    initrd   /initramfs-linux.img
    options  "root=UUID=c42c79b5-559e-48b5-8738-dc0c8af43d63 rw quiet initrd=intel-ucode.img"
    submenuentry "Boot using fallback initramfs" {
        initrd initramfs-linux-fallback.img
    }
    submenuentry "Boot to terminal" {
        add_options "systemd.unit=multi-user.target"
    }
}
```
这里options后为内核参数，UUID指的是根目录GUID，Intel CPU要加内核参数`initrd=intel-ucode.img`，这里的`intel-ucode.img`在`ESP`分区下

  
