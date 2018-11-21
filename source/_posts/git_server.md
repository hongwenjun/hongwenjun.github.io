---
title: 体验腾讯云-开发者实验  搭建 Git 服务器
date: 2018-3-28
tags:  git
---


##  体验腾讯云-开发者实验  搭建 Git 服务器

![](https://share-10039692.file.myqcloud.com/lab/ac197229e6/logo/svyp4cez8d/git.svg)
Git 是一款免费、开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。
此实验以 CentOS 7.2 x64 的系统为环境，搭建 git 服务器。

### 腾讯云-开发者实验室
[https://cloud.tencent.com/developer/labs/gallery](https://cloud.tencent.com/developer/labs/gallery)

### 网页打链接，找到搭建Git服务器，
开始学习测试，没有帐号的可以用微信扫描登陆。可以在浏览器中内嵌的SSH工具完成所有的安装测试工作.
	
	# 推荐使用 passwd 修改 root 密码，记录下 vps 机器的ip，自己使用SSH登陆
	  passwd    //改密码
	# 本地电脑 打开 soft\Git\git-bash.exe 开启终端
	  ssh root@139.199.167.50
	
### 安装依赖库和编译工具
为了后续安装能正常进行，我们先来安装一些相关依赖库和编译工具

	yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel

安装编译工具

	yum install gcc perl-ExtUtils-MakeMaker


### 下载 git
选一个目录，用来放下载下来的安装包，这里将安装包放在 /usr/local/src 目录里

	cd /usr/local/src

到官网找一个新版稳定的源码包下载到 /usr/local/src 文件夹里

	wget https://www.kernel.org/pub/software/scm/git/git-2.10.0.tar.gz

### 解压和编译

解压下载的源码包

	tar -zvxf git-2.10.0.tar.gz

解压后进入 git-2.10.0 文件夹

	cd git-2.10.0

执行编译

	make all prefix=/usr/local/git
	
	# 测试的时候直接编译错误，先运行配置，再更新了安装的库
	./configure

编译完成后, 安装到 /usr/local/git 目录下

	make install prefix=/usr/local/git
	
### 配置环境变量
将 git 目录加入 PATH,将原来的 PATH 指向目录修改为现在的目录

	echo 'export PATH=$PATH:/usr/local/git/bin' >> /etc/bashrc

生效环境变量

	source /etc/bashrc

此时我们能查看 git 版本号，说明我们已经安装成功了。

	git --version

### 创建 git 账号密码
创建 git 账号
为我们刚刚搭建好的 git 创建一个账号

	useradd -m gituser
	
然后为这个账号设置密码

	passwd gituser

### 初始化 git 仓库并配置用户权限
创建 git 仓库并初始化
我们创建 /data/repositories 目录用于存放 git 仓库

	mkdir -p /data/repositories
	
创建好后，初始化这个仓库

	cd /data/repositories/ && git init --bare test.git

### 配置用户权限
给 git 仓库目录设置用户和用户组并设置权限

	chown -R gituser:gituser /data/repositories
	chmod 755 /data/repositories

查找 git-shell 所在目录
 , 编辑 /etc/passwd 文件，将最后一行关于 gituser 的登录 shell 配置改为 git-shell 的目录

	vim /etc/passwd
	gituser:x:500:500::/home/gituser:/usr/local/git/bin/git-shell


### 使用搭建好的 Git 服务
克隆 test repo 到本地，本地电脑开另一个终端

	cd ~ && git clone gituser@139.199.167.50:/data/repositories/test.git
	# ip 为测试云主机的ip
	
### 实际测试 SSH 终端命令记录
![](/img/git_server.png)