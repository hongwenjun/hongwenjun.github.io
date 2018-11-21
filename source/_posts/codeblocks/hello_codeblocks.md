---
title: Hello CodeBlocks! “正确打开方式”
date: 2018-04-15  10:01
tags:  CodeBlocks
---

https://github.com/hongwenjun/CodeBlocks

蘭雅sRGB 龙芯小本服务器 | [sRGB.vicp.net](http://sRGB.vicp.net)

---

## CodeBlocks视频_新建项目_复制代码_编译运行

这才是“正确打开方式”，如果hello world都没法编译运行，可以分析的构建记录，知道是否编译器设置错误，
或者是新的操作系统WIN10(自带杀毒软件麦咖啡，导致没法编译)的权限不够，导致不能编译可执行文件。

![](/webp/cb/hello_codeblocks.webp)

很多新手，不建立项目，直接编辑源文件 我的程序.c 就开始运行，然后说没法运行，什么破软件，然后。。。
这不是“正确打开方式”，只有建立项目，才能方便编译，调试。

一个项目只能有一个 mian函数，如果你有多个小练习放一个项目了，可以进入命令行，手工编译运行

## 解决问题: 下载版本没有集成GCC编译器

我们应该选择官网 [www.codeblocks.org](http://www.codeblocks.org/)
找到下载页面: [http://www.codeblocks.org/downloads/binaries](http://www.codeblocks.org/downloads/binaries)
选择集成GCC 编译器的版本，下载安装，可以选
codeblocks-17.12mingw-setup.exe  或者 codeblocks-17.12mingw-nosetup.zip

## 如果你不想重新下载，也可以单独安装下载TDM-GCC
[tdm-gcc.tdragon.net](http://tdm-gcc.tdragon.net/download)
CodeBlocks里集成的c/c++编译器，就使用使用tdm-gcc，你可以在这里选择下载x86 或者 x64 的GCC编译器

## 如果可能以上资源被墙了，你还可以其他推荐获得帮助
CodeBlocks+wxWidgets QQ群号: 158607753
可以到群文件里下载  CodeBlocks_17.12_sRGB增强版

### 百度盘，虽然经常失效，(设置密码是为了保鲜)
CodeBlocks_17.12_sRGB增强版
链接: https://pan.baidu.com/s/1jbo0ra7hKc11QE1yudvplA 密码: xgi2

CodeBlocks加EasyX图形库 (集成vc2010和EasyX，你可以替换CB新版升级)
链接:https://pan.baidu.com/s/1n_VRA-LJemLMUX829FXQ-g 密码:11h8

CodeBlocks视频教程
https://pan.baidu.com/s/1hqozPxM

## 如果win10操作系统权限不够
尝试删除自带杀毒软件麦咖啡，给CB程序增加权限


## 其他容易产生的问题
请不要安装中文目录下，或者带有空格等目录下
主要是gcc编译程序的时候，可能会莫名其妙的问题
推荐安装  C:\CodeBlocks 或者  D:\CodeBlocks 方便定置使用

## 新手进阶网址
自力更生丰衣足食，自己配置CodeBlocks!

![](/webp/cb/tips.webp)

## 使用git下载  CodeBlocks 配置目录说明和个性配置文件
```
git clone https://github.com/hongwenjun/CodeBlocks.git  CodeBlocks

```
