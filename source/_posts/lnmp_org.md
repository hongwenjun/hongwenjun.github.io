---
title: 虚拟主机 VPS 一键安装LNMP教程
date:  2018-11-5
tags:  vps
---

### 远程登陆主机，可以ssh 或者 putty  xshell等

	ssh root@144.202.95.95
	按提示输入密码,控制台 可以shift + insert 粘贴

### 先修改密码方便自己

	passwd

### 安装 tmux 后台服务和多窗口工具

	apt-get  update
	apt-get install tmux

### 安装 LNMP 一键安装包，登陆 lnmp.org
	
- 或者直接到这个URL，选择配置自动安装脚本

    https://lnmp.org/auto.html

```
wget http://soft.vpser.net/lnmp/lnmp1.5.tar.gz -cO lnmp1.5.tar.gz && \
tar zxf lnmp1.5.tar.gz && cd lnmp1.5 && \
LNMP_Auto="y" DBSelect="2" DB_Root_Password="lnmp.org" \
InstallInnodb="y" PHPSelect="5" SelectMalloc="1" ./install.sh lnmp
```

### 后台安装方法

1. 先输入命令 tmux ，开启后台服务管理进程
2. shift + insert 粘贴 把lnmp安装脚本，然后就可以默认安装了
3. 可以直接关闭远程登陆软件，vps会自己安装了
4. 安装都是下载源码编译，要不少时间，可以 tmux a 接入上去查看


### 安装好 lnmp 后控制台输入 lnmp管理
```
root@568315379:~/lnmp1.5# lnmp
+-------------------------------------------+
|    Manager for LNMP, Written by Licess    |
+-------------------------------------------+
|              https://lnmp.org             |
+-------------------------------------------+
Usage: lnmp {start|stop|reload|restart|kill|status}
Usage: lnmp {nginx|mysql|mariadb|php-fpm|pureftpd} {start|stop|reload|restart|kill|status}
Usage: lnmp vhost {add|list|del}
Usage: lnmp database {add|list|edit|del}
Usage: lnmp ftp {add|list|edit|del|show}
Usage: lnmp ssl add
Usage: lnmp {dnsssl|dns} {cx|ali|cf|dp|he|gd|aws}
root@568315379:~/lnmp1.5#
```

- lnmp 安装好后，最好安装下 pureftpd 服务，lnmp 可以管理ftp帐号

		./pureftpd.sh
- lnmp 可以  Usage: lnmp ftp {add|list|edit|del|show} 管理ftp帐号

### LNMP 建立虚拟主机 ，管理 www.xxx.net 主页

	lnmp vhost add 
