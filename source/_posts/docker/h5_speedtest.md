---
title: 使用Docker安装HTML5-Based Speedtest,测试下网络高峰访问自己网站的速度
date:  2020-11-06
tags:  docker
---

## HTML5-Based Speedtest on Docker

### 0. 特别说明
- 由于Speedtest会尽可能使用最大的带宽，来反馈最真实的网络性能，所以，在部署完成项目后，请不要将你的测速地址分享给其他人或者公开到群/论坛/贴吧等处！ 因此导致的流量损失、超流量停机，甚至欠费，iLemonrain (以下简称镜像作者)将不负任何责任！



### 1. 镜像说明
网页版Speedtest 却测试不出来本地到目标服务器的速度？

服务器上跑 Speedtest-CLI 却总感觉测试结果不靠谱？

现在，有了 HTML5-Based Speedtest on Docker ，这一切都迎刃而解！

(更要命的是居然还Docker化了？真正的一键部署测速环境！)

### 2. 镜像Tag
- Docker镜像：ilemonrain/html5-speedtest

- html5-speedtest, html5-speedtest:latest：默认Speedtest镜像，默认为Alpine Linux内核

- html5-speedtest:alpine：Alpine Linux内核

### 3. 使用方法
- 启动命令行：

```
docker run [-t/-d] -p [6688]:80 ilemonrain/html5-speedtest:latest
```
- 参数详解：

```
-t：启动后显示日志，可用Ctrl+C转入后台运行
-d：后台模式启动
-p 6688:80：镜像映射端口，修改6688为任意端口即可
```
之后访问 http://你的服务器IP地址:镜像映射端口/ ，即可愉快的开始测速啦~

- 示例命令：
```
docker run -d -p 8888:80 ilemonrain/html5-speedtest:alpine
```

---

### Docker Pull Command
```
docker pull ilemonrain/html5-speedtest
```
### 晚上8点多种，在自己的一个服务器上跑了下速度
![](/img/docker/h5_speedtest.png)

---
### Dockerfile

```
FROM alpine

LABEL MAINTAINER iLemonrain <ilemonrain@ilemonrain.com>

RUN (apk --no-cache upgrade ;\
     apk add php7-apache2 curl php7-cli php7-json php7-phar php7-openssl php7-mbstring php7-zlib ;\
     curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer ;\
     sed -i "s/AllowOverride none/AllowOverride All/" /etc/apache2/httpd.conf ;\
     rm -f /var/www/localhost/htdocs/* ;\
     mkdir /run/apache2/ ;\
     rm -f /var/cache/apk/* )

ADD entrypoint.sh /entrypoint.sh
ADD speedtest/* /var/www/localhost/htdocs/

RUN (chown -R apache:apache /var/www/localhost/htdocs/ ;\
     chmod 755 /entrypoint.sh )

EXPOSE 80

ENTRYPOINT [ "sh", "/entrypoint.sh" ]
```

- 大概阅读Dockerfile，镜像好像安装了 php7和apache2，网页代码是 ** https://getcomposer.org/installer **
这个脚本安装，使用 ** entrypoint.sh **启动web，主要命令是 ** httpd -D FOREGROUND **

```
## 使用命令进入容器查看
docker exec  -it exciting_hertz  sh

```
## 网页程序5个文件
```
/var/www/localhost/htdocs
-rw-r--r--    1 apache   apache         231 Apr 16  2018 empty.php
-rw-r--r--    1 apache   apache         870 Apr 16  2018 garbage.php
-rw-r--r--    1 apache   apache        2955 Apr 16  2018 getIP.php
-rw-r--r--    1 apache   apache        7186 Apr 16  2018 index.html
-rw-r--r--    1 apache   apache       10846 Apr 16  2018 speedtest_worker.min.js

```
