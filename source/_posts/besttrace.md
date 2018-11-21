---
title: 使用BestTrace查看VPS的去程和回程
date:  2018-11-5
tags:  vps
---
### vps上可以运行一键脚本，检测到国内各大节点的路由路线

```
wget -qO- git.io/besttrace | bash
```
### besttrace.sh 测试效果图

![](/webp/besttrace.webp)

脚本会下载 besttrace 程序到本地
接下来可以 使用命令检测vps到你你的本地ip的路线 -q 1 表示测试一次

```
./besttrace  119.6.6.6
./besttrace  -q 1  119.6.6.6
```
### 自己从ipip.net下载其他版本，好像缺少龙芯 mips64 芯片支持
-  vim  mybesttrace.sh  
```
#!/bin/bash

#  IPv4 免费地址库 & 客户端工具
#  包括IPv4 免费数据库及相关、IP库解析代码第三方版、BestTrace 软件下载、浏览器扩展
#  https://www.ipip.net/download.html#ip_trace
#  https://cdn.ipip.net/17mon/besttrace4linux.zip

# 下载安装 besttrace
mkdir -p besttrace  && cd besttrace  && \
wget https://cdn.ipip.net/17mon/besttrace4linux.zip && \
unzip besttrace4linux.zip && chmod +x besttrace 

# 金华电信
./besttrace  -q  1 115.212.100.211
```

### 网上也有windows的版本
https://www.bandwagonhost.net/1186.html
- 或者网页版 
https://www.ipip.net/

### git.io/besttrace 是个短网址
https://raw.githubusercontent.com/zq/shell/master/autoBestTrace.sh
```
#!/bin/bash

# apt -y install unzip

# install besttrace
if [ ! -f "besttrace" ]; then
    wget https://github.com/zq/shell/raw/master/besttrace
    # unzip besttrace4linux.zip
    chmod +x besttrace
fi

## start to use besttrace

next() {
    printf "%-70s\n" "-" | sed 's/\s/-/g'
}

clear
next

ip_list=(14.215.116.1 101.95.120.109 117.28.254.129 113.207.32.65 119.6.6.6 183.192.160.3 183.221.253.100 202.112.14.151)
ip_addr=(广州电信 上海电信 厦门电信 重庆联通 四川联通 上海移动 成都移动 成都教育网)
# ip_len=${#ip_list[@]}

for i in {0..7}
do
	echo ${ip_addr[$i]}
	./besttrace -q 1 ${ip_list[$i]}
	next
done
```
