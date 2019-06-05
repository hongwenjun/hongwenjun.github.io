---
title: debian 软件源-国内镜像中科大和清华大学
date:  2019-6-3
tags:  [linux]
---

### 中科大源
https://mirrors.ustc.edu.cn/repogen/

### 清华大学源
https://mirrors.tuna.tsinghua.edu.cn/
```
deb http://mirrors.ustc.edu.cn/debian/ stretch main contrib non-free
deb-src http://mirrors.ustc.edu.cn/debian/ stretch main contrib non-free

deb http://mirrors.ustc.edu.cn/debian/ stretch-updates main contrib non-free
deb-src http://mirrors.ustc.edu.cn/debian/ stretch-updates main contrib non-free

deb http://mirrors.ustc.edu.cn/debian/ stretch-backports main contrib non-free
deb-src http://mirrors.ustc.edu.cn/debian/ stretch-backports main contrib non-free

deb http://mirrors.ustc.edu.cn/debian-security/ stretch/updates main contrib non-free
deb-src http://mirrors.ustc.edu.cn/debian-security/ stretch/updates main contrib non-free
```

### 软件源没有证书，使用apt-key注册证书
	apt-key adv --recv-keys --keyserver keyserver.ubuntu.com EF0F382A1A7B6500

### 使用 Debian mipsel DVD 光盘做软件源
- 搜索 debian-8.10.0-mipsel-DVD-1.iso 能否找到看人品
- 推荐使用国外的VPS，下载镜像，挂载在web目录
- wget https://cdimage.debian.org/cdimage/archive/8.10.0/mipsel/iso-dvd/debian-8.10.0-mipsel-DVD-1.iso

```
# 临时做软件源 下载ISO 加载  mount -o loop debian-8.10.0-mipsel-DVD-1.iso debian
# 编辑 vim /etc/apt/sources.list
deb http://srgb18.ga/debian/debian/ jessie main contrib
deb http://srgb18.ga/debian/ jessie main contrib
```