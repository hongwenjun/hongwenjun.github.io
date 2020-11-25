---
title: MSYS2 中国镜像使用帮助
date:  2020/11/25
tags:  msys2
---

蘭雅sRGB 龙芯2F服务器和博客 | [https://262235.xyz](https://262235.xyz)
---

### MSYS2 镜像使用帮助
```
收录架构
MINGW: i686, x86_64
MSYS: i686, x86_64
安装
请访问该镜像目录下的 distrib/ 目录（x86_64 、i686），找到名为 msys2-<架构>-<日期>.exe 的文件（如 msys2-x86_64-20141113.exe），下载安装即可。

pacman 的配置
编辑 /etc/pacman.d/mirrorlist.mingw32 ，在文件开头添加：

Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/mingw/i686
编辑 /etc/pacman.d/mirrorlist.mingw64 ，在文件开头添加：

Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/mingw/x86_64
编辑 /etc/pacman.d/mirrorlist.msys ，在文件开头添加：

Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/msys/$arch

然后执行 pacman -Sy 刷新软件包数据即可。
```

### 安装 fish
```
#  pacman -S fish
正在解析依赖关系...
正在查找软件包冲突...

软件包 (6) bc-1.07.1-2  groff-1.22.4-1  libpcre2_16-10.35-1  libpipeline-1.5.2-1  man-db-2.9.3-1  fish-3.1.2-1

下载大小：   2.92 MiB
全部安装大小：  30.61 MiB

```
