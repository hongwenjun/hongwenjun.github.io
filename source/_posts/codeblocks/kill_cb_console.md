---
title: CodeBlocks 突然没法编译运行的问题
date: 2018-04-14  21:41
tags:  CodeBlocks
---

# CodeBlocks 突然没法编译运行的问题

https://github.com/hongwenjun/CodeBlocks

蘭雅sRGB 个人博客 | [https://262235.xyz](https://262235.xyz)

---

运行程序后只能关闭黑框或者按任意键结束程序,
如果直接点工作栏上的红色中止按钮，就会出现图上的情况。
生成和运行按钮全部灰掉，点运行会显示编译器还在运行中
直接关闭codeblocks会显示正在编译，是否结束编译关闭
选是的话codeblocks会无响应然后强制关闭.

# 知道了CB怎么运行用户的程序，应该知道问题的原因了
![](/img/cb_console.jpg)
先看图，我来解释，举例 编译的程序是 123.exe
----
绿色运行按钮 执行的命令

- 正在执行： "cb_console_runner.exe" "123.exe"

红色调试运行按钮 执行的命令

- 启动调试器: gdb32.exe -nx -fullname -quiet -args 123.exe
----

目前版本17.12，可能权限不够 直接点工作栏上的红色中止按钮，并不能真的关闭程序，
只是把窗口隐藏起来，还是可以在任务管理器查到没有停止的 123.exe 和 cb_console_runner.exe
所有发现不能使用 绿色运行按钮，请检测 windows 任务管理器 是否有遗留进程

# 在工具菜单里添加一个功能，就可以方便解决问题
![](/webp/cb/kill_cb_console_runner.webp)

如演示图，填入下面命令到对应位置，然后就可以使用了
```
工具名称: Kill_CB_Console_Runner
执行命令: taskkill.exe
参数: /im ${PROJECT_NAME}.exe /f /im cb_console_runner.exe

```

