### 在此目录打开 CMD 命令提示符

将下面内容保存为`.reg`文件后导入注册表。

```reg
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Classes\Directory\background\shell\cmd_here]

@="在此处打开CMD窗口"
"Icon"="cmd.exe"

[HKEY_LOCAL_MACHINE\SOFTWARE\Classes\Directory\background\shell\cmd_here\command]

@="\"C:\\Windows\\System32\\cmd.exe\""


[HKEY_LOCAL_MACHINE\SOFTWARE\Classes\Folder\shell\cmdPrompt]

@="在此处打开CMD窗口"


[HKEY_LOCAL_MACHINE\SOFTWARE\Classes\Folder\shell\cmdPrompt\command]

@="\"C:\\Windows\\System32\\cmd.exe\" \"cd %1\""


[HKEY_LOCAL_MACHINE\SOFTWARE\Classes\Directory\shell\cmd_here]

@="在此处打开CMD窗口"
"Icon"="cmd.exe"


[HKEY_LOCAL_MACHINE\SOFTWARE\Classes\Directory\shell\cmd_here\command]

@="\"C:\\Windows\\System32\\cmd.exe\""
```