---
title: 使用DoxyBlocks自动函数简短注释
date:  2018-04-16  21:58
tags:  CodeBlocks
---
https://github.com/hongwenjun/CodeBlocks

蘭雅sRGB 个人博客 | [https://262235.xyz](https://262235.xyz)
---

请确认DoxyBlocks插件是否已经启用，如果启用会有下图视频中的DoxyBlocks工具栏。

定位到你要注释的函数申明语句,全选一行;点下 /** 按钮，就能帮你提取参数生成模版了。


![](/webp/cb/doxyblocks.webp)

##   Doxygen 注释说明
```c
/** \brief 函数的简短注释
 *
 * \param  参数的简短注释
 * \param  参数2
 * \return 返回值的简短注释
 *
 */

// 函数申明实例
/** \brief  复制字符串from 中的字符到字符串to
 *
 * \param to char*   目标字符串
 * \param from const char*   源字符串
 * \return char*    返回值为指针to
 *
 */
char *strcpy( char *to, const char *from );

 ```
