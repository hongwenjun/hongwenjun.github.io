---
title: 国人编译的GCC,支持中文帮助信息
date: 2018-10-8
tags:  [gcc]
---

蘭雅sRGB 龙芯小本服务器 | [sRGB.vicp.net](http://sRGB.vicp.net)

![](/webp/gcc-mcf.webp)

### 国人编译的GCC支持中文信息 主页
https://gcc-mcf.lhmouse.com/   

###  作者 github
https://github.lhmouse.com/

### 设置方法
- 下载最新的把版本，解压到对应目录

	C:\CodeBlocks\

- 环境变量 用户 PATH 添加

	C:\CodeBlocks\MinGW64\bin;

- 运行 CMD 开启窗口，输入 gcc -v 就可以使用
- 也可以在 CodeBlocks 设置对应的编译器

### 不添加path变量使用
- 建立文件 C:\CodeBlocks\MinGW6\mingwvars.bat
```
@echo.
@echo Setting up environment for using GCC with the MCF thread model from %~dp0.
@set PATH=%~dp0bin;%PATH%

```