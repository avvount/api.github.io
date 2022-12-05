---
title: Arch安装配置sublime text 3
date: 2018-01-04 10:37:19
tags:
    - Arch
---
# 安装
1. Install the GPG key  

    `curl -O https://download.sublimetext.com/sublimehq-pub.gpg && sudo pacman-key --add sublimehq-pub.gpg && sudo pacman-key --lsign-key 8A8F901A && rm sublimehq-pub.gpg `

2. Select the channel to use  

- Stable  
`echo -e "\n[sublime-text]\nServer = https://download.sublimetext.com/arch/stable/x86_64" | sudo tee -a /etc/pacman.conf`
- Dev  
`echo -e "\n[sublime-text]\nServer = https://download.sublimetext.com/arch/dev/x86_64" | sudo tee -a /etc/pacman.conf`  

3. Update pacman and install Sublime Text  

    `sudo pacman -Syu sublime-text`  

# 中文输入法  
> git clone https://github.com/lyfeyaj/sublime-text-imfix.git  
cd sublime-text-imfix  
./sublime-imfix  

# 插件  
> chineselocalizations  
Codecs33  
converttoutf8  
package control  
sublimerepl  
ALL Autocomplete  
CoolFormat  
HexViewer  
MasmAssembly  
SublimeAStyleFormatter  
SublimeBashTidy  
SublimeGit  
Terminal  


  
