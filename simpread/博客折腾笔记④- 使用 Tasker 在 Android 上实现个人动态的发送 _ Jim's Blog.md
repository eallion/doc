\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[jimlee2002.github.io\](https://jimlee2002.github.io/posts/4394c3fa.html)

[前情提要](https://jimlee2002.github.io/posts/2b426e0a.html)

折腾了两天，我终于是实现在 Android 上使用 Tasker 向刚搭建好的个人动态系统发送内容了。

这是一个在 Android 上向[废话胶囊（b 言 b 语）](https://github.com/daibor/nonsense.fun)发送内容的简单 Tasker 工程。

项目地址：[https://github.com/jimlee2002/nonsense.fun\_tasker](https://github.com/jimlee2002/nonsense.fun_tasker)

[![](https://i.loli.net/2020/04/22/Hy7kwJL8FDr6I5O.png)](https://i.loli.net/2020/04/22/Hy7kwJL8FDr6I5O.png)

[¶](#直接下载安装已经导出好的apk文件) 直接下载安装已经导出好的 [apk 文件](https://github.com/jimlee2002/nonsense.fun_tasker/releases)
---------------------------------------------------------------------------------------------------------

应用使用插件`Tasker App Factory`导出。

注意，该应用**需要 root 权限**。

[¶](#导入Tasker工程) 导入 Tasker 工程
-----------------------------

**注意：部分手机可能需要 Root 权限才能使用，该工程默认开启`使用Root运行`，可以自行到`场景/Main/发送/按下`的第 6 个和第 8 个任务里关掉该选项**。

[![](https://i.loli.net/2020/04/22/iaTO5gAQLjnufBZ.png)](https://i.loli.net/2020/04/22/iaTO5gAQLjnufBZ.png)[![](https://i.loli.net/2020/04/22/SIJivZ5L4Na9Cu3.png)](https://i.loli.net/2020/04/22/SIJivZ5L4Na9Cu3.png)

[![](https://i.loli.net/2020/04/24/c1R3x9HEzyQiTpN.png)](https://i.loli.net/2020/04/24/c1R3x9HEzyQiTpN.png)[![](https://i.loli.net/2020/04/22/7BoIjaJL9h6ilf1.png)](https://i.loli.net/2020/04/22/7BoIjaJL9h6ilf1.png)

1.  [下载](https://github.com/jimlee2002/nonsense.fun_tasker/releases)`bb.prj.xml`，存入到手机任意你找得到的位置。
    
2.  下载安装 Tasker。
    
3.  进入主界面长按左下角的按钮，点击`导入项目`，在打开的界面中找到并打开刚才存入的`bb.prj.xml。`
    
    [![](https://i.loli.net/2020/04/22/mpwnk2ZWvMc6uSU.png)](https://i.loli.net/2020/04/22/mpwnk2ZWvMc6uSU.png)[![](https://i.loli.net/2020/04/22/3Zc2KIWVfBzhiDM.png)](https://i.loli.net/2020/04/22/3Zc2KIWVfBzhiDM.png)
    
    > 提示：点击右下角的手机按钮可以快速回到内部储存空间目录
    
4.  完成后回到主界面，点击应用栏里图标长得和 Tasker 很像的`Tasker Secondary`，打开界面。
    
    [![](https://i.loli.net/2020/04/22/Gju9BY64UsWlvTw.png)](https://i.loli.net/2020/04/22/Gju9BY64UsWlvTw.png)[![](https://i.loli.net/2020/04/22/Hy7kwJL8FDr6I5O.png)](https://i.loli.net/2020/04/22/Hy7kwJL8FDr6I5O.png)
    
5.  **长按**发送按钮，打开设置页面进行必要设置。
    
    [![](https://i.loli.net/2020/04/22/YM5CJ6vb4OIdemy.png)](https://i.loli.net/2020/04/22/YM5CJ6vb4OIdemy.png)
    
    **Title：** 这里是发送界面顶端的文字，请随意修改。
    
    **AppID、MasterKey：** 网页打开 LeanCloud，在你的项目里点击`设置/应用Keys`，复制对应的密钥分别填入。
    
    [![](https://i.loli.net/2020/04/20/Kaxt5GOo3LRgMmy.png)](https://i.loli.net/2020/04/20/Kaxt5GOo3LRgMmy.png)
    
    **className：** 一般是`content`，只要你是按照[少数派的指南](https://sspai.com/post/60024)来做的话。
    
    **–insecure：** 是否在脚本命令末尾加上`--insecue`。参数默认关闭，如果无法发送可以尝试打开这个选项试试。
    
    **完成后点击确认返回**。
    

这样就配置完成了，请试试看吧！

[¶](#通过-Tasker-Secondary-打开) 通过 Tasker Secondary 打开
---------------------------------------------------

[![](https://i.loli.net/2020/04/22/Gju9BY64UsWlvTw.png)](https://i.loli.net/2020/04/22/Gju9BY64UsWlvTw.png)

[¶](#通过桌面小工具创建快捷方式打开) 通过桌面小工具创建快捷方式打开
-------------------------------------

1.  打开 Tasker，然后**点击返回键**回到主界面。
    
2.  在桌面上新建 Tasker 的桌面小部件 "任务"，在打开的界面选择`Show UI`,
    
    在界面下方选择图标，然后点击左上角返回桌面。
    
    [![](https://i.loli.net/2020/04/22/QWRPd7IKmV3oXYj.png)](https://i.loli.net/2020/04/22/QWRPd7IKmV3oXYj.png)[![](https://i.loli.net/2020/04/22/t5dlHRyUgDM7aKX.png)](https://i.loli.net/2020/04/22/t5dlHRyUgDM7aKX.png)
    
    完成，现在你应该能看到快捷方式了。
    

[¶](#自行导出为APK安装) 自行导出为 APK 安装
-----------------------------

\*\* 注意：你必须拥有手机的 Root 权限，并勾选`场景/Main/发送/按下`的第 6 个和第 8 个任务中的`使用Root运行`选项 \*\*

1.  Google Play 安装`Tasker App Factory`。
    
2.  打开 Tasker，主界面左下方长按选择已经导入的项目，然后选择`导出\作为应用。`
    
    [![](https://i.loli.net/2020/04/22/peARXFgoinvOJzx.png)](https://i.loli.net/2020/04/22/peARXFgoinvOJzx.png)
    
    > 提示：你可以通过点击`更名`重命名工程名称来修改应用名。
    
    [![](https://i.loli.net/2020/04/22/TZzLONjeHJviCp5.png)](https://i.loli.net/2020/04/22/TZzLONjeHJviCp5.png)
3.  根据提示输入包名和版本号。
    
    [![](https://i.loli.net/2020/04/22/Q7nXMpqxhB5o8a3.png)](https://i.loli.net/2020/04/22/Q7nXMpqxhB5o8a3.png)
4.  点击左上角返回，Tasker 会将项目以 APK 格式导出到`内部储存/Tasker/factory/kids`并安装。
    

界面如果有问题可以自行在 Tasker 的`场景`中修改。

个人能力有限，做的比较粗糙，还请不吝赐教！

感谢 [daibor](https://github.com/daibor) 制作了这么棒的[项目。](https://github.com/daibor/nonsense.fun)

感谢少数派的 @SoSo 在评论下分享的方法启发了这个工程。