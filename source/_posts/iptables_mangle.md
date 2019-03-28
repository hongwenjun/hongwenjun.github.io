---
title: 路由器使用 iptables 限制 玩客云上传数据流量
date: 2019-3-28
tags:  [iptables]
---

蘭雅sRGB 龙芯小本服务器 | [sRGB.vicp.net](http://sRGB.vicp.net)

### 路由器使用 iptables 限制 玩客云上传数据流量
```
### 限制玩客云设备  192.168.1.90 每秒钟通过 20×1.5=30K ；超过的流量都丢弃
iptables -t mangle -I FORWARD 1 -s 192.168.1.90  -m limit --limit 20/s --limit-burst 100 -j ACCEPT
iptables -t mangle -A FORWARD -s 192.168.1.90 -j DROP

# 查询限速命令是否生效
iptables -t mangle  -nvL  FORWARD
```
### 查询 iptables -t mangle 结果
```
/home/root # iptables -t mangle  -nvL  FORWARD
Chain FORWARD (policy ACCEPT 6460 packets, 2683K bytes)
 pkts bytes target     prot opt in     out     source               destination
 3381  408K ACCEPT     all  --  *      *       192.168.1.90         0.0.0.0/0            limit: avg 20/sec burst 100
  379 54868 DROP       all  --  *      *       192.168.1.90         0.0.0.0/0
```
### 路由器里开机脚本设置
![](/img/iptables_mangle.png)


### 原理说明：
- 参考文章 http://bbs.xiaomi.cn/t-32602219

![](/img/FORWARD.jpg)

iptables本身并没有限速指令，但可以通过limit指令匹配包速率，溢出部分使用DROP指令丢弃，从而变相实现限速功能，需要注意规则的顺序。

正常都是内网主机接路由器访问外网，根据iptables数据包的流程图来看，数据包是路过路由器，只需要转发数据，

所以我们需要在FORWARD链上执行限速。 而FORWARD链在mangle表和filter表里。根据我测试结果来看，路由器pro需要在mangle表上做限速设置，下面给出具体限速指令

比如我给局域网的一台主机 IP地址为 192.168.31.23的限速 1.5MB。

iptables -t mangle -I FORWARD 1 -s 192.168.31.23 -m limit --limit 1000/s --limit-burst 1500 -j ACCEPT

iptables -t mangle -A FORWARD -s 192.168.31.23 -j DROP

--limit 1000/s ：这个是说每秒种只允许通过1000个IP包，一个IP包大约在1.5KB， 1000个也就是1.5M，具体限速多少，可以根据这个来计算，比如我想限速4.5MB/S, 那就是设置 --limit 3000/S 

--limit-burst 1500： 这个是初始值，开始有1500包可以直接通过，后续就每秒1000个包。

执行命令后，可以查询一下是否正常写入了。

iptables -t mangle  -n -v -L  FORWARD   

限速是时实生效的，命令执行成功后，限速就生效了，这个限速策略是保存在内存里的，重启会消失的，需要保存指令。
