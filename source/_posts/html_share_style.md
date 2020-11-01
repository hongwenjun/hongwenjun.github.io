---
title: tohtml_style 共享样式工具
date: 2018-03-18
tags:  [cpp]
---

蘭雅sRGB 个人博客  https://262235.xyz
	
https://github.com/hongwenjun/tohtml_style

# tohtml_style
1. 先使用 VIM 的 TOhtml 把文本转换成 html
```
vim -c :TOhtml -c :wqa  mycode.cpp
vim -c :TOhtml -c :wqa  mydoc.txt
```

2. 再使用本工具 html_share_style 把编辑好的样式共享给 html文件
```
Usage: html_share_style  <file.html>  <from.html>
```
![](https://raw.githubusercontent.com/hongwenjun/tohtml_style/master/usage.webp)



# 附送  git-bash环境设置使用TDM-GCC 64
```
    编辑 Git\etc\fstab
    添加一行(填入对应GCC路径)
    C:/CodeBlocks/MinGW64       /mingw64
```
![](https://raw.githubusercontent.com/hongwenjun/tohtml_style/master/git-bash_gcc.png)

# 附送 .vimrc
" .vimrc   请把本文件 _vimrc 改成 .vimrc 放到 ~目录
