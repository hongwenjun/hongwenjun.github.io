---
title: CodeBlocks 帮助手册设置更新
date: 2018-08-3 
tags:  CodeBlocks
---

https://github.com/hongwenjun/CodeBlocks

蘭雅sRGB 龙芯小本服务器 | [sRGB.vicp.net](http://sRGB.vicp.net)

---


![](/webp/cb/help.webp)


## 使用git下载  CodeBlocks 配置目录说明和个性配置文件
```
git clone https://github.com/hongwenjun/CodeBlocks.git  CodeBlocks

```


### 学习C/C++ 最好用的帮助手册

[cplusplus-2013-8-8.chm](https://github.com/hongwenjun/CodeBlocks/raw/master/CHM/cplusplus-2013-8-8.chm)

### CB 帮助手册文档设置

文本保存help.xml，然后使用 cb_share_config.exe 导入到默认设置里

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes" ?>
<CodeBlocksConfig version="1">
<help_plugin>
<DEFAULT int="3" />
<BASE_FONT_SIZE int="10" />
<help0>
    <NAME>
        <str>
            <![CDATA[www.cplusplus.com在线搜索]]>
        </str>
    </NAME>
    <FILE>
        <str>
            <![CDATA[http://www.cplusplus.com/search.do?q=$(keyword)]]>
        </str>
    </FILE>
    <ISEXEC bool="0" />
    <EMBEDDEDVIEWER bool="0" />
    <KEYWORDCASE int="0" />
    <DEFAULTKEYWORD>
        <str>
            <![CDATA[]]>
        </str>
    </DEFAULTKEYWORD>
</help0>
<help1>
    <NAME>
        <str>
            <![CDATA[Google翻译文本]]>
        </str>
    </NAME>
    <FILE>
        <str>
            <![CDATA[http://translate.google.cn/?q=$(keyword)]]>
        </str>
    </FILE>
    <ISEXEC bool="0" />
    <EMBEDDEDVIEWER bool="0" />
    <KEYWORDCASE int="0" />
    <DEFAULTKEYWORD>
        <str>
            <![CDATA[]]>
        </str>
    </DEFAULTKEYWORD>
</help1>
<help2>
    <NAME>
        <str>
            <![CDATA[Cpp标准库函数中文手册]]>
        </str>
    </NAME>
    <FILE>
        <str>
            <![CDATA[$(CODEBLOCKS)\chm\c++库函数中文.chm]]>
        </str>
    </FILE>
    <ISEXEC bool="0" />
    <EMBEDDEDVIEWER bool="0" />
    <KEYWORDCASE int="0" />
    <DEFAULTKEYWORD>
        <str>
            <![CDATA[]]>
        </str>
    </DEFAULTKEYWORD>
</help2>
<help3>
    <NAME>
        <str>
            <![CDATA[Cplusplus 2013.8.8]]>
        </str>
    </NAME>
    <FILE>
        <str>
            <![CDATA[$(CODEBLOCKS)\chm\cplusplus-2013-8-8.chm]]>
        </str>
    </FILE>
    <ISEXEC bool="0" />
    <EMBEDDEDVIEWER bool="0" />
    <KEYWORDCASE int="0" />
    <DEFAULTKEYWORD>
        <str>
            <![CDATA[]]>
        </str>
    </DEFAULTKEYWORD>
</help3>
<help4>
    <NAME>
        <str>
            <![CDATA[MSDN精简版]]>
        </str>
    </NAME>
    <FILE>
        <str>
            <![CDATA[$(CODEBLOCKS)\chm\vc.chm]]>
        </str>
    </FILE>
    <ISEXEC bool="0" />
    <EMBEDDEDVIEWER bool="0" />
    <KEYWORDCASE int="0" />
    <DEFAULTKEYWORD>
        <str>
            <![CDATA[]]>
        </str>
    </DEFAULTKEYWORD>
</help4>
<help5>
    <NAME>
        <str>
            <![CDATA[MSDN 1.5 精简安装版]]>
        </str>
    </NAME>
    <FILE>
        <str>
            <![CDATA[C:\CodeBlocks\tool\msdn.exe $(keyword)]]>
        </str>
    </FILE>
    <ISEXEC bool="1" />
    <EMBEDDEDVIEWER bool="0" />
    <KEYWORDCASE int="0" />
    <DEFAULTKEYWORD>
        <str>
            <![CDATA[]]>
        </str>
    </DEFAULTKEYWORD>
</help5>
<help6>
    <NAME>
        <str>
            <![CDATA[Cppreference_2017]]>
        </str>
    </NAME>
    <FILE>
        <str>
            <![CDATA[$(CODEBLOCKS)\chm\cppreference_2017.chm]]>
        </str>
    </FILE>
    <ISEXEC bool="0" />
    <EMBEDDEDVIEWER bool="0" />
    <KEYWORDCASE int="0" />
    <DEFAULTKEYWORD>
        <str>
            <![CDATA[]]>
        </str>
    </DEFAULTKEYWORD>
</help6>
</help_plugin>
</CodeBlocksConfig>
```