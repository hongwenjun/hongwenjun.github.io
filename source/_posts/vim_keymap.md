---
title: VIM 命令键盘全图-中文清晰
date: 2019-3-27
tags:  [vim]
---

## VIM 命令键盘全图-中文清晰
蘭雅sRGB 个人博客 [https://262235.xyz](https://262235.xyz)


![](https://raw.githubusercontent.com/hongwenjun/img/master/VIM_KEY_CN.png)

----   
### VIM 常用用法 

|一般模式    |              编辑模式     |         指令模式    | 
| --------   | :------                  | :-----             |
|h   左      |          a,i,r,o,A,I,R,O       | :w   保存 |
|j   下      |         进入编辑模式           | :w!   强制保存 |
|k   上      |         dd   删除光标当前行    | :q!   不保存离开 |
|l   右      |         ndd   删除n行          | :wq!   保存后离开 |
|0   移动到行首   |   yy   复制当前行         | :e!   还原原始档 |
|$   移动到行尾   |   nyy   复制n行           | :w   filename   另存为 |
|H   屏幕最上     |     p,P   粘贴            | :set  nu   设置行号 |
|M   屏幕中央     |     u     撤消            | :set  nonu   取消行号 |
|L   屏幕最下     | [Ctrl]+r   重做上一个动作 | ZZ   保存离开 |
|G   文件最后一行 | [ctrl]+z   暂停退出       | :set nohlsearch 永久地关闭高亮显示 |
|/work   向下搜索 |                           | :sp   同时打开两个文档   |
|?work   向上搜索 |                           | [Ctrl]+w   两个文档设换 |
|gg   移动到文件第一行     |                   | :nohlsearch  暂时关闭高亮显示 |


#### vim 格式化代码命令是等号 = 
    全部格式化 : gg=G  对当前行格式化(缩进): ==
    删除所有行文字 ggdG 或者 :%d
    ctrl+p或者ctrl+n  代码自动补全功能

#### 表示位置的元字符
    $  匹配行尾
    ^  匹配行首
    \< 匹配单词词首
    \> 匹配单词词尾

    删除行尾的^M：%s/\r//g     
    删除行尾空格：%s/\s+$//g   
    删除行首多余空格：%s/^\s*//
    删除沒有內容的空行：%s/^$//


#### 快捷键来激活/取消 paste模式
    set pastetoggle=<F11>  

#### 实际操作组合命令
![](http://srgb.xyz/webp/vim_cmd.webp)
1. 先按i插入模式, 再键盘 F11 切换粘贴模式  
2. shift + Insert (做视频时笔误) 从windows 把文本粘贴进去
3. 删除行首的行号：%s/^.\d//g
4. 删除行首多余空格：%s/^\s*//g
5. gg 到文件首行, d6 删除6行
6. gg=G 格式化代码,  ggdG 全删文字    


