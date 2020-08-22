\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[blog.51cto.com\](https://blog.51cto.com/wenzhongxiang/2349585)

在使用 notepad++ 工具的时候，很多情况下我们会遇到批量替换空行的操作，之前的操作方法是快捷键 Crtl+h 调出窗口选择替换栏，在查找目标栏中输入 \\ r\\n\\r\\n，替换为 栏中输入 \\ r\\n 并选择全部替换，可实现批量删除空行的操作。随着 Visual Studio Code 的普及，之前 notepad++ 好多内容想在 vs code 中实现，其中最常用的删除空行也是很有必要学习的。

在 VS Code 中我们可以通过 Ctrl+h 快捷键调出替换界面，在替换查找界面输入空行对应的正则表达式 ^\\s\*(?=\\r?$)\\n 并 Alt+R 选择对应正则表达式查找模式，批量全部替换即可完成需求，具体如下：

1\. 快速打开替换界面，在 Find 界面输入 ^\\s\*(?=\\r?$)\\n

2.Alt+R 选择 Use Regular Expression(Alt+R) 即正则表达式模式：

3\. 选择 Replace All(Ctrl+Alt+Enter) 批量替换全部完成操作，截图如下：

[![](https://s1.51cto.com/images/blog/201902/12/d7edd21def264571b48061e7cf91ca62.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)](https://s1.51cto.com/images/blog/201902/12/fcf6531903245d1a7d6bc6d5f92e3072.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

**常用快捷键补充：**

快捷键汇总：可通过 Ctrl+K Ctrl+S 快速打开，或者通过 File→Preferences→Keyboard Shortcuts 打开：

[![](https://s1.51cto.com/images/blog/201902/12/35d01c1bb24efa04b6ac2206e5243e24.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)](https://s1.51cto.com/images/blog/201902/12/48b788a2e2316dc8b5d8848e08a95972.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)  
当前行快速换行：Ctrl+Enter  
快速删除某一行：Shift+Delete 或者 Ctrl+Shift+K  

查找：Ctrl+F

文件中查找：Ctrl+Shift+F

替换：Ctrl+H  
文件中替换：Ctrl+Shift+H

其他快捷方式后续再补充吧

欢迎关注微信公众号：小温研习社  

![](https://s1.51cto.com/images/20190519/1558230539363484.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)