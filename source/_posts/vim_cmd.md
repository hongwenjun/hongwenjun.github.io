---
title: VIM 常用用法和linux常用命令
date: 2018-3-23
tags:  [vim,linux]
---

## VIM 常用用法和linux常用命令
蘭雅sRGB 个人博客 [https://262235.xyz](https://262235.xyz)

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

----

#### tar 命令参数和示例
    -c: 建立压缩文件    -x：解压   -t：查看内容
    -r：向压缩归档文件末尾追加文件 -u：更新原压缩包中的文件
    
- tar -cvf  /home/123.tar  my.cpp  打包，不压缩
- tar -zcvf  /home/123.tar.gz  my.cpp  打包gz压缩
- tar -xvf  123.tar            解开包
- tar -zxvf /home/123.tar.gz   以gzip解压
- tar -jxvf /home/123.tar.bz2  以bzip2解压
- tar -ztvf /tmp/etc.tar.gz    查看tar内容

----

#### chmod 命令用来变更文件或目录的权限
    Linux用户分为：拥有者、组群(Group)、其他（other）
    r=读取属性　read=4
    w=写入属性　write=2
    x=执行属性　execute=1
    
- chmod  755  list.sh      // 设定脚本执行权限
- chmod -R 755  mypath     // 递归设定目录权限 

----
crontab 定时任务 [e]编辑,[l]显示,[r]删除任务 
history  | grep vim  列出有关vim的编辑的历史文件

----

##  Hexo环境迁移
实现方法：在Hexo仓库新建一个hexo分支存放Hexo原始文件，master分支存放hexo生成的静态页面，如果迁移环境后可以直接git clone仓库即可。



1. 将Hexo仓库用git管理起来：
```
# 注意：不需要再编写.gitignore了，在Hexo工程已经默认有.gitignore文件了，
# 这是hexo默认生成的，也许是hexo本来就推荐用git管理hexo原始文件吧
git init
git checkout -b hexo
git add .
git commit -m "init"
git remote add origin https://github.com/hongwenjun/hongwenjun.github.io.git
git push origin hexo
```


2. 在新的环境克隆仓库

```
git clone https://github.com/hongwenjun/hongwenjun.github.io.git
# 切换到hexo分支即可看到hexo原始文件，此时可以编辑并提交。
# 一般先提交原始文件到hexo分支，然后hexo d部署生成的静态文件到master分支
git checkout hexo

```
