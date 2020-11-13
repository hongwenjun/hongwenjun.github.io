---
title: Debian10安装远程桌面和最新Code::Blocks 20.03 For linux版本
date: 2020/11/13
tags:  CodeBlocks
---

蘭雅sRGB 个人博客 | [https://262235.xyz](https://262235.xyz)


## Xrdp - 通过Windows mstsc 的RDP连接Linux远程桌面
```
# 安装 Xrdp
apt install xrdp
systemctl enable xrdp
systemctl restart xrdp

# 安装 xfce4 图形桌面，配置xrdp
sudo apt-get install xfce4
echo xfce4-session > ~/.xsession
touch .session
vim /etc/xrdp/startwm.sh

# 在文件startwm.sh最前面添加
xfce4-session
# 然后重启 xrdp 服务
systemctl restart xrdp

```

## debian安装最新版Code::Blocks 20.03

```
# 下载解压安装包
wget http://sourceforge.net/projects/codeblocks/files/Binaries/20.03/Linux/Debian%2010/codeblocks_20.03_amd64_stable.tar.xz

tar xfv codeblocks_20.03_amd64_stable.tar.xz

#安装库
apt install libwxgtk3.0-dev -y
dpkg -i *.deb

# 安装过程中如果 ldconfig 错误
export PATH=/usr/loca/sbin:/usr/sbin:/sbin:$PATH

#再次完成codeblocks安装
dpkg -i  *.deb

#安装编译器等
apt install -y git gettext build-essential autoconf libtool automake
```
