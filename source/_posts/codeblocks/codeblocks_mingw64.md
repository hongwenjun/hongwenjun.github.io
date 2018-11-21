---
title: Code::Blocks 2018 增强版 中文美化 CPP语法文档 多编译器支持
date: 2018-10-13
tags:  CodeBlocks
---

蘭雅sRGB 龙芯小本服务器 | [sRGB.vicp.net](http://sRGB.vicp.net)

## Code::Blocks 2018 增强版 By 蘭雅sRGB
**百度盘下载**  https://pan.baidu.com/s/1osEHZZPBXh_AppKblTHD4A

### 官方下载的 codeblocks免安装版
- **codeblocks-17.12mingw-nosetup.zip**

### 中文化，美化主题，CPP帮助文档，编译器设置
- 文件 **CodeBlocks中文化美化增强包.zip**


### Mingw-w64  GCC for Windows 64bits
- GCC 版本 8.1 支持 最新的C++标准
- 文件 **MinGW64_GCC_8.1.7z**

### 附送 VC2015 编译器
-文件 **MSVC2015Mini.7z**

### 更新修改中CB设置，放到CodeBlocks目录下就可以用
- 文件 **default.conf**

<pre>
----------目前发现的小BUG-----------------------

1. Mingw-w64 8.1  GDB调试 for循环  STL容器中有非ASCII(中文)字符，会转码错误
   gdb错误日志 Python Exception <type 'exceptions.UnicodeEncodeError'> 'ascii' 
   codec can't encode characters in position 10-11: 

2. 使用Mingw-w64建立 w64项目，冷启动CodeBlocks 首次重新打开就 w64项目， 
   NativeParser :: CreateParser()：创建C++语法解析器会错误
   解决方法:1)关系w64项目，重新再重新打开w64项目  
            2)新建一个临时的w64项目，再打开旧w64项目
</pre>

![](/webp/cb/help.webp)

### CodeBlocks 更多使用技巧
http://srgb.vicp.net/tags/CodeBlocks/

**github项目**   https://github.com/hongwenjun/CodeBlocks