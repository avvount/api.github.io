---
title: Arch系统备份与还原
date: 2018-01-04 10:35:12
tags:
    - Arch
---
# arch系统备份与还原  

## 备份
- 安装pigz  
`sudo pacman -S pigz`  
- 执行以下命令  
`sudo tar --use-compress-program=pigz -cvpf /home/beta/Documents/arch-backup.tgz --exclude=/boot --exclude=/home --exclude=/proc --exclude=/dev --exclude=/sys --exclude=/tmp --exclude=/run --exclude=/lost+found --exclude=/mnt --exclude=/media --exclude=/var/lock --exclude=/var/run --exclude=/var/cache/pacman/pkg /`  

## 还原  
- 从安装光盘/U盘启动
* `sudo nano /etc/pacman.d/mirrorlist `配置源  
- 安装pigz  
- 挂载根分区到`/mnt`  
- `rm -rf /mnt/*` （慎重）  
- 解压  
`tar --use-compress-program=pigz -xvpf /f/sysbackup/arch-backup.tgz -C /mnt`  
- 挂载home boot等分区
- 生成fstab  
`genfstab -U /mnt > /mnt/etc/fstab`  
- arch-chroot到`/mnt`  
- 重建grub
> grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=arch  
grub-mkconfig -o /boot/grub/grub.cfg  


  
