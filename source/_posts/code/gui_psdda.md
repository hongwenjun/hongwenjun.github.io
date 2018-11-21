---
title: 图形界面_PSD大文件垃圾数据清理工具
date: 2018-8-3
tags:  [cpp]
---

蘭雅sRGB 龙芯小本服务器  http://sRGB.vicp.net
	
https://github.com/hongwenjun/cmd_gui

### 图形界面_PSD大文件垃圾数据清理工具

使用方法见图

![](/webp/guida.webp)

### 源代码片段

窗口程序就是接收程序名和参数，组合成一行命令行
然后去隐藏调用

```cpp
bool CALLBACK runBtnClick(HELE hEle, HELE hEventEle)
{

    // 文本框回写配置
    edit_text();

    // 格式化命令行
    wchar_t wbuf [2 * MAX_PATH] = {0};
    char cmdline[2 * MAX_PATH] = {0};
    swprintf(wbuf, L"\"%s\" \"%s\"  %s\\" , appFile, docFile, fontPath);
    WCHARTochar(cmdline, wbuf);

    MessageBoxA(NULL, cmdline, "注意: 确认目录存在,不能有空格", MB_OKCANCEL);
    execute_command(cmdline);


    return true;
}


// 执行命令行
int execute_command(char* cmdline)
{
    SetConsoleTitle(cmdline);
    STARTUPINFO si;
    PROCESS_INFORMATION pi;
    ZeroMemory(&si, sizeof(si));
    si.cb = sizeof(si);

    // 后台隐藏
    si.dwFlags   =   STARTF_USESHOWWINDOW;
    si.wShowWindow   =   SW_HIDE;

    ZeroMemory(&pi, sizeof(pi));
    // Start the child process.
    CreateProcess(NULL, TEXT(cmdline), NULL, NULL, FALSE, 0,
                  NULL, NULL, &si, &pi);
    // Wait until child process exits.
    WaitForSingleObject(pi.hProcess, INFINITE);
    // Get the return value of the child process
    DWORD ret;
    GetExitCodeProcess(pi.hProcess, &ret);
    if (!ret) {
        MessageBoxA(NULL, "PSD大文件垃圾清理工具执行完成!",
                    "(C) 版权所有 2018.08 Hongwenjun (蘭公子)", MB_OKCANCEL);
    }
    // Close process and thread handles.
    CloseHandle(pi.hProcess);
    CloseHandle(pi.hThread);
    return ret;
}

```

