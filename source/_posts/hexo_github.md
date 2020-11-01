---
title: Hexo 使用 github 编写个人博客
date: 2018-11-21
tags:  [hexo]
---

蘭雅sRGB 个人博客 [https://262235.xyz](https://262235.xyz)

----   

##  Hexo 使用 github 里编写个人博客
实现方法：在Hexo仓库新建一个hexo分支存放Hexo原始文件，master分支存放hexo生成的静态页面，如果迁移环境后可以直接git clone仓库即可。


1. 将Hexo仓库用git管理起来，新建一个hexo分支用来存markdown文件
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

2. ssh 登陆 vps，进入webroot目录，把博客从github上拉到vps

```
cd /var/www  && rm /var/www/html
git clone https://github.com/hongwenjun/hongwenjun.github.io.git   html

# 博客如果更新了，在vps上运行
cd /var/www/html  && git pull

```
[![](https://github.com/hongwenjun/hongwenjun.github.io/raw/hexo/source/img/hexo_github_1.jpg)](https://youtu.be/KF6dalUw5Eg)]


3. 在新的环境克隆仓库

```
git clone https://github.com/hongwenjun/hongwenjun.github.io.git
# 切换到hexo分支即可看到hexo原始文件，此时可以编辑并提交。
# 一般先提交原始文件到hexo分支，然后hexo d部署生成的静态文件到master分支
git checkout hexo

```
