---
title: git bash 命令行有中文乱码的解决
date: 2018-5-18
tags:  [git]
---

蘭雅sRGB 龙芯小本服务器 [http://sRGB.vicp.net](http://srgb.vicp.net)


网上有把MINGW64环境改成GBK的方法，但是哪样使用习惯不太好，毕竟网络世界utf-8是主宰。

### 解决方法:命令前添加 winpty

	$   winpty ping  192.168.1.1
	$   winpty ipconfig

### 编辑文件，添加
	$ vim ~/.bashrc

	# MINGW64(git_bash) 解决 ping 和 ipconfig 乱码
	alias ping='_win_ping() { winpty ping $@ ; }; _win_ping'
	alias ipconfig='_win_ipconfig() { winpty ipconfig $@ ; }; _win_ipconfig'



### 在 git bash 里运行 java 命令，打印出的中文显示乱码
可以在java命令行之前添加 winpty

	$   winpty java
