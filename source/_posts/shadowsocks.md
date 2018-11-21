---
title: shadowsocks 客户端安装
date: 2018-5-21
tags:  [shadowsocks]
---

蘭雅sRGB 龙芯小本服务器 | [sRGB.vicp.net](http://sRGB.vicp.net)
	
# 手机下载安装
shadowsocks android手机 [下载地址](https://github.com/shadowsocks/shadowsocks-android/releases)

https://github.com/shadowsocks/shadowsocks-android/releases

安装后，填实际的帐号参数

	服务器：188.188.188.188
	端口：2018
	密码：teddysun.com
	加密方式：aes-256-cfb

### 苹果手机使用app可以选用免费的 wingy

---

# Shadowsocks Windows 使用说明(转)
[原文](https://github.com/shadowsocks/shadowsocks-windows/wiki)
#### 功能

1. 系统代理设置
2. PAC 模式和全局模式
3. [GFWList] 和用户规则
4. 支持 HTTP 代理
5. 支持多服务器切换
6. 支持 UDP 代理
7. 支持插件

#### 下载

下载 [最新版]。

需要安装 [.NET Framework 4.6.2] 和 Microsoft [Visual C++ 2015 Redistributable] (x86)

从 2.5.8 开始你可以在 Releases 页面找到 exe 文件的 hash 值，你可以使用 [fciv](https://support.microsoft.com/en-us/kb/841290) 等工具 校验 `Shadowsocks.exe` 文件. 例如 `fciv.exe -both -add Shadowsocks.exe`

#### 基本使用

1. 在任务栏找到 Shadowsocks 图标
2. 在 服务器 菜单添加多个服务器
3. 选择 `启用系统代理` 来启用系统代理。请禁用浏览器里的代理插件，或把它们设置为使用系统代理。
4. 除了设为系统代理，你也可以直接自己配置浏览器代理。在 [SwitchyOmega] 中把代理设置为 SOCKS5 或 HTTP 的 127.0.0.1:1080。这个 1080 端口可以在服务器设置中设置。

#### PAC

1. 可以编辑 PAC 文件来修改 PAC 设置。Shadowsocks 会监听文件变化，修改后会自动生效。
2. 你也可以从 [GFWList] （由第三方维护）更新 PAC 文件。
3. 你也可以使用在线 PAC URL

#### 服务器自动切换

1. 负载均衡：随机选择服务器
2. 高可用：根据延迟和丢包率自动选择服务器
3. 累计丢包率：通过定时 ping 来测速和选择。如果要使用本功能，请打开菜单里的`统计可用性`。
4. 也可以实现 IStrategy 接口来自定义切换规则，然后给我们发一个 pull request。

#### UDP

对于 UDP，请使用 SocksCap 或 ProxyCap 强制你想使用的程序走代理。

#### 多实例

如果想使用其它工具如 [SwitchyOmega] 管理多个服务器，可以启动多个 Shadowsocks。
为了避免配置产生冲突，把 Shadowsocks 复制到一个新目录里，并给它设置一个新的本地端口。

#### 插件

若想通过插件来连接服务器，请到编辑服务器界面填入插件程序（相对路径或绝对路径）

_注意：_ 在启用插件后，正向代理会被停用。

#### 全局快捷键

如果重启 Shadowsocks 则必须**重新注册**，因为此时环境可能发生变化，而且如果多开 Shadowsocks 则需要为后来启动的实例设置不同的快捷键。

##### 怎样键入快捷键?

1. 点击想要设置的快捷键文本框。
2. 按下想要设置的组合键。
3. 当满足要求时释放全部按键。
4. 这时你输入的快捷键字符会出现在文本框中。

##### 如何修改快捷键?

1. 点击想要设置的快捷键文本框。
2. 按下 BackSpace（退格键）清除文本框内容。
3. 重新键入新的组合键。

##### 如何取消激活?

1. 清除你想要取消激活快捷键的文本框内容，如果想要取消全部，则清除全部文本框中的内容。
2. 点击确认按钮。

##### 标签背景色含义

- 绿色: 此组合键未被其他程序占用，并且成功注册到系统里。
- 黄色: 此组合键已被其他程序占用，你需要更换其他组合。
- 透明无色: 初始状态

#### 服务器配置

请访问 [服务器] 获取更多信息。

#### 开发

需要 [Visual Studio 2015] 或更高版本并安装 [.NET Framework 4.6.2 Developer Pack]。

#### 授权

[GPLv3]

#### 项目所使用到的第三方开源组件/库

```
Caseless.Fody (MIT)    https://github.com/Fody/Caseless
Costura.Fody (MIT)     https://github.com/Fody/Costura
Fody (MIT)             https://github.com/Fody/Fody
GlobalHotKey (GPLv3)   https://github.com/kirmir/GlobalHotKey
Newtonsoft.Json (MIT)  https://www.newtonsoft.com/json
StringEx.CS ()         https://github.com/LazyMode/StringEx
ZXing.Net (Apache 2.0) https://github.com/micjahn/ZXing.Net

libsscrypto (GPLv2)    https://github.com/shadowsocks/libsscrypto
Privoxy (GPLv2)        https://www.privoxy.org
Sysproxy ()            https://github.com/Noisyfox/sysproxy
```

[Appveyor]:       https://ci.appveyor.com/project/celeron533/shadowsocks-windows
[Build Status]:   https://ci.appveyor.com/api/projects/status/tfw57q6eecippsl5/branch/master?svg=true
[最新版]: https://github.com/shadowsocks/shadowsocks-windows/releases
[服务器]:        https://github.com/shadowsocks/shadowsocks/wiki/Ports-and-Clients#linux--server-side
[SwitchyOmega]:  https://github.com/FelisCatus/SwitchyOmega
[GFWList]:        https://github.com/gfwlist/gfwlist
[.NET Framework 4.6.2]: https://www.microsoft.com/zh-CN/download/details.aspx?id=53344
[Visual Studio 2015]: https://www.visualstudio.com/downloads/
[.NET Framework 4.6.2 Developer Pack]: https://www.microsoft.com/download/details.aspx?id=53321
[Visual C++ 2015 Redistributable]: https://www.microsoft.com/en-us/download/details.aspx?id=53840
[GPLv3]:        https://github.com/shadowsocks/shadowsocks-windows/blob/master/LICENSE.txt