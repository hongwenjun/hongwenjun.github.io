---
title: Linux 终端 使用 tmux 分屏
date: 2018-10-9
tags:  [vim]
---

蘭雅sRGB 龙芯小本服务器 | [sRGB.vicp.net](http://sRGB.vicp.net)

![](/webp/tmux.gif)

### 安装tmux工具
	apt-get install tmux

### 使用工具 tmux 分屏, 每次都要先按 Ctrl+b
1. 输入命令 tmux 使用工具
2. 上下分屏：Ctrl+b  再按 "
3. 左右分屏：Ctrl+b  再按 %
4. 切换屏幕：Ctrl+b  再按o
5. 关闭一个终端：Ctrl+b  再按x
6. 上下分屏与左右分屏切换： Ctrl+b  再按空格键

### tmux 其他操作
    可以使用 ctrl+a+d 退出 tmux 终端，这个比较通用
    tmux窗口选择：Ctrl+b 再按 ←↑→↓光标键选择
    Ctrl+b c   创建新窗口(桌面)
    Ctrl+b 0~9 选择几号窗口(桌面)
    Ctrl+b ? 显示快捷键帮助
    Ctrl+b C-o 调换窗口位置，类似与vim 里的C-w
    Ctrl+b 空格键 采用下一个内置布局
    Ctrl+b ! 把当前窗口变为新窗口
    Ctrl+b " 模向分隔窗口
    Ctrl+b % 纵向分隔窗口
    Ctrl+b q 显示分隔窗口的编号
    Ctrl+b o 跳到下一个分隔窗口
    Ctrl+b 上下键 上一个及下一个分隔窗口
    Ctrl+b ALT-方向键 调整分隔窗口大小
    Ctrl+b n 选择下一个窗口
    Ctrl+b l 切换到最后使用的窗口
    Ctrl+b p 选择前一个窗口
    Ctrl+b w 以菜单方式显示及选择窗口
    Ctrl+b t 显示时钟
    Ctrl+b ; 切换到最后一个使用的面板
    Ctrl+b x 关闭面板
    Ctrl+b & 关闭窗口
    Ctrl+b s 以菜单方式显示和选择会话
    Ctrl+b d 退出tumx，并保存当前会话，这时，
          tmux仍在后台运行，可以通过
          tmux attach进入 到指定的会话
          
![](/img/tmux.png)

###  .tmux.conf 设定
```
# https://www.youtube.com/watch?v=xTplsyQaGFs

# tmux 启用鼠标操作
setw -g mouse
set-option -g history-limit 20000
set-option -g mouse on
bind -n WheelUpPane select-pane -t= \; copy-mode -e \; send-keys -M
bind -n WheelDownPane select-pane -t= \; send-keys -M
```
![](/webp/tmux_mouse.gif)
