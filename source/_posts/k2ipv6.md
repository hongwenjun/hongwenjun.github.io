---
title: 浙江移动光纤支持IPV6了
date: 2019-02-24
tags:  [ipv6]
---

蘭雅sRGB 个人博客 | [https://262235.xyz](https://262235.xyz)

### K2路由器如下设置，启用ipv6，可以获取ipv6地址
![](/img/k2ipv6.png)


### 自动获取的DNS，可以手动添加到网卡设置里
	2409:8028:2000::1111
	2409:8028:2000::2222

### google ipv6 dns:
	2001:4860:4860::8888
	2001:4860:4860::8844

```
$ ping 2001:4860:4860::8888

正在 Ping 2001:4860:4860::8888 具有 32 字节的数据:
来自 2001:4860:4860::8888 的回复: 时间=242ms
来自 2001:4860:4860::8888 的回复: 时间=241ms
来自 2001:4860:4860::8888 的回复: 时间=231ms
来自 2001:4860:4860::8888 的回复: 时间=246ms

2001:4860:4860::8888 的 Ping 统计信息:
    数据包: 已发送 = 4，已接收 = 4，丢失 = 0 (0% 丢失)，
往返行程的估计时间(以毫秒为单位):
    最短 = 231ms，最长 = 246ms，平均 = 240ms

```


### IPV6_note.TXT
```
#停用“ip helper”服务
net stop "ip helper"

#启用“ip helper”服务
net start "ip helper"

#显示Teredo信息
netsh interface ipv6 show teredo

#Teredo、6to4、isatap重置
netsh interface teredo set state default
netsh interface 6to4 set state default
netsh interface isatap set state default

#关闭和卸载Teredo、6to4、isatap
netsh interface teredo set state disable
netsh interface 6to4 set state disabled
netsh interface isatap set state disabled

#重新启用Teredo
netsh interface Teredo set state type=default

#设置Teredo服务器
netsh interface teredo set state server=teredo.remlab.net
netsh interface teredo set state server=teredo-debian.remlab.net
netsh interface teredo set state server=teredo.trex.fi

#设置Teredo服务器为teredo.ipv6.microsoft.com（此teredo服务器报废）
netsh interface ipv6 set teredo client teredo.ipv6.microsoft.com

#设置isatap服务器（PING不通）
netsh int IPV6 isatap set router isatap.scu.edu.cn

#手动解决Windows7对IPv6支持的瑕疵
netsh interface IPV6 set global randomizeidentifiers=disabled

#启用Teredo
netsh interface ipv6 set teredo enterpriseclient
netsh int ter set state enterpriseclient

#手动换算（IPv4）并设置本地连接（IPv6）地址
#换算IPv4地址
http://ip-lookup.net/conversion.php
#修改本地连接IPv6地址
#子网前缀长度 48

#google ipv6 dns:
2001:4860:4860::8888
2001:4860:4860::8844

#opendns ipv6 dns:
2620:0:ccc::2
2620:0:ccd::2

#HE ipv6 dns:
2001:470:20::2

ipconfig /all
ipconfig /flushdns
netsh int ipv6 show int
netsh int ipv6 show route

#看看teredo状态是不是qualified
netsh int ipv6 show teredo

#删除多余回路
route DELETE ::/0

#添加路由 (这一步重启后需要重新再做一遍)
netsh int ipv6 add route ::/0 "Teredo Tunneling Pseudo-Interface"

#在“start.bat”中添加下面两句，实现XX执行自启
netsh int ipv6 add route ::/0 "Teredo Tunneling Pseudo-Interface"
SET PYTHONPATH="%~dp0%start.vbs" console

#优先级
netsh int ipv6 show prefix
netsh int ipv6 set prefix 2002::/16 30 1
netsh int ipv6 set prefix 2001::/32 5 1

#查看Teredo Tunneling Pseudo-Interface 接口
route print

#显示IPv6地址
netsh interface ipv6 show address

#显示IPv6路由
netsh interface ipv6 show route

#重启ipv6，再重启计算机
netsh interface ipv6 reset

#重启网卡（"本地连接 2"换成自己要重启的网卡名）
netsh interface set interface "本地连接 2" disabled
netsh interface set interface "本地连接 2" enabled

#IPV6测试网站：

http://test-ipv6.com/
#摘要部分测试完成后，请到“测试项目”中查看结果。
#全是“成功”就最完美的。

http://www.kame.net/kame-mosaic.html
#IPv6可以看到活动的乌龟，IPv4乌龟不动
```