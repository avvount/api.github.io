---
title: Arch安装步骤
date: 2018-01-01 09:56:11
tags:
    - Arch
---
## 有线网络执行`systemctl start dhcpcd`,无线执行`wifi-menu`链接wifi
## 更新系统时间 `timedatectl set-ntp true`
## 分区
## 格式化根分区 mkfs.ext4 /dev/sda#
## 挂载分区
>mount /dev/sda7 /mnt
mkdir /mnt/boot
mount /dev/sda2 /mnt/boot
mkdir /mnt/home
mount /dev/sda6 /mnt/home

## 编辑 `/etc/pacman.d/mirrorlist`
## 安装基本系统
`pacstrap /mnt base base-devel`
## 生成fstab
`genfstab -U /mnt > /mnt/etc/fstab`
## change root到新系统
`arch-chroot /mnt`
## 设置时区
> ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
hwclock --systohc --utc

## 设置语言
编辑`/etc/locale.gen`
执行`locale-gen`
## 执行`echo LANG=en_US.UTF-8 > /etc/locale.conf`
## 设置主机名
> echo Archpc >> /etc/hostname
echo "127.0.0.1	Archpc.localdomain Archpc" >> /etc/hosts

## 安装必要软件
`pacman -S gvim net-tools wireless_tools wpa_supplicant dialog intel-ucode os-prober grub efibootmgr openssh linux-headers`

## 编辑 `/etc/lvm/lvm.conf`
设置set use_lvmetad = 1 为 use_lvmetad = 0
## 安装grub
> grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=grub
grub-mkconfig -o /boot/grub/grub.cfg

## 设置root密码 & 添加普通用户
> useradd -m -G wheel beta
set beta password
visudo

## 其他配置

#### 安装桌面环境
- 安装必要软件包
`pacman -S xorg-xinit xf86-video-intel`
- 安装gnome桌面
`pacman -S gnome`
执行echo `"exec gnome-session" >> ~/.xinitrc`后可通过startx命令进入桌面
- 设置中文
startx进入中文桌面
`echo "export LANG=zh_CN.UTF-8" >> ~/.xinitrc`
桌面管理器进入中文桌面(最新gnome例外)
`echo "export LANG=zh_CN.UTF-8" >> ~/.xprofile`

#### 安装nvidia驱动
> pacman -S nvidia bumblebee bbswitch
echo "blacklist nouveau" >> /etc/modprobe.d/blacklist.conf

重启



#### 设置fcitx输入法,将以下三行内容分别写入~/.xinitrc和~/.xprofile(gnome需写入/etc/environment)中
> export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx

#### 启用multilib仓库
编辑 /etc/pacman.conf，取消下面内容的注释：
> [multilib]
Include = /etc/pacman.d/mirrorlist

#### 启用archlinuxcn源
在/etc/pacman.conf中添加：
> [archlinuxcn]
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch


  
