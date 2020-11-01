---
title: CodeBlocks 调试器设置 更新
date:  2018-8-3 
tags:  CodeBlocks
---
https://github.com/hongwenjun/CodeBlocks

蘭雅sRGB 个人博客 | [https://262235.xyz](https://262235.xyz)
---

## 安装调试器gdb或cdb
- tdmgcc编译器已经自带gdb调试器

- cdb调试器 百度搜索 WinDbg
- WinDbg最新官方版下载_百度软件中心  点击 普通下载, 千万不要点高速下载

## gdb和cdb 分别建立配置

![如果看不到图片，请用chrome或者安卓手机浏览器](/webp/cb/gdb_cdb_gcc_vc.webp)

## 编译器中选择对应调试器设置
以下文本保存成  gdb.xml 再使用 cb_share_config.exe 工具导入到配置里
```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes" ?>
<CodeBlocksConfig version="1">
<debugger_common>
<sets>
<gdb_debugger>
<conf1>
<NAME>
    <str>
        <![CDATA[Default]]>
    </str>
</NAME>
<values>
    <EXECUTABLE_PATH>
        <str>
            <![CDATA[$(CODEBLOCKS)\MinGW\bin\gdb32.exe]]>
        </str>
    </EXECUTABLE_PATH>
    <DISABLE_INIT bool="1" />
    <USER_ARGUMENTS>
        <str>
            <![CDATA[]]>
        </str>
    </USER_ARGUMENTS>
    <TYPE int="0" />
    <INIT_COMMANDS>
        <str>
            <![CDATA[source $(TARGET_COMPILER_DIR)gdb32\bin\gdbinit
]]>
        </str>
    </INIT_COMMANDS>
    <WATCH_ARGS bool="1" />
    <WATCH_LOCALS bool="1" />
    <CATCH_EXCEPTIONS bool="1" />
    <EVAL_TOOLTIP bool="1" />
    <ADD_OTHER_SEARCH_DIRS bool="0" />
    <DO_NOT_RUN bool="0" />
    <DISASSEMBLY_FLAVOR int="1" />
    <INSTRUCTION_SET>
        <str>
            <![CDATA[]]>
        </str>
    </INSTRUCTION_SET>
</values>
</conf1>
<conf2>
<NAME>
    <str>
        <![CDATA[cdb]]>
    </str>
</NAME>
<values>
    <EXECUTABLE_PATH>
        <str>
            <![CDATA[C:\CodeBlocks\tool\windbg\cdb.exe]]>
        </str>
    </EXECUTABLE_PATH>
    <DISABLE_INIT bool="1" />
    <USER_ARGUMENTS>
        <str>
            <![CDATA[]]>
        </str>
    </USER_ARGUMENTS>
    <TYPE int="1" />
    <INIT_COMMANDS>
        <str>
            <![CDATA[]]>
        </str>
    </INIT_COMMANDS>
    <WATCH_ARGS bool="1" />
    <WATCH_LOCALS bool="1" />
    <CATCH_EXCEPTIONS bool="1" />
    <EVAL_TOOLTIP bool="1" />
    <ADD_OTHER_SEARCH_DIRS bool="0" />
    <DO_NOT_RUN bool="0" />
    <DISASSEMBLY_FLAVOR int="0" />
    <INSTRUCTION_SET>
        <str>
            <![CDATA[]]>
        </str>
    </INSTRUCTION_SET>
</values>
</conf2>
<conf3>
<NAME>
    <str>
        <![CDATA[MinGW64_GDB]]>
    </str>
</NAME>
<values>
    <EXECUTABLE_PATH>
        <str>
            <![CDATA[$(CODEBLOCKS)\MinGW64\bin\gdb64.exe]]>
        </str>
    </EXECUTABLE_PATH>
    <DISABLE_INIT bool="1" />
    <USER_ARGUMENTS>
        <str>
            <![CDATA[]]>
        </str>
    </USER_ARGUMENTS>
    <TYPE int="0" />
    <INIT_COMMANDS>
        <str>
            <![CDATA[source $(TARGET_COMPILER_DIR)gdb64\bin\gdbinit
]]>
        </str>
    </INIT_COMMANDS>
    <WATCH_ARGS bool="1" />
    <WATCH_LOCALS bool="1" />
    <CATCH_EXCEPTIONS bool="1" />
    <EVAL_TOOLTIP bool="0" />
    <ADD_OTHER_SEARCH_DIRS bool="0" />
    <DO_NOT_RUN bool="0" />
    <DISASSEMBLY_FLAVOR int="0" />
    <INSTRUCTION_SET>
        <str>
            <![CDATA[]]>
        </str>
    </INSTRUCTION_SET>
</values>
</conf3>
</gdb_debugger>
</sets>
</debugger_common>
</CodeBlocksConfig>

```

### 测试包含中文的调试用示例代码

```cpp
#include <iostream>
#include <map>
#include <string>

using namespace std;
int main()
{
    map<string, int> mymap = {
        {"张三", 60},   {"李四", 65}, {"王五", 75}
    };

    string admiral[3] = { "张飞",  "关羽",  "吕布" };

    mymap.insert(pair<string, int>(admiral[0], 98));
    mymap.insert(pair<string, int>(admiral[1], 97));
    mymap.insert(pair<string, int>(admiral[2], 99));

    for (auto it = mymap.begin(); it != mymap.end(); ++it)
        cout << it->first << " => " << it->second << '\n';


    return 0;
}
```