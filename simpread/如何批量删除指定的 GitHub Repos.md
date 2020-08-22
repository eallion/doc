\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[juejin.im\](https://juejin.im/post/6844903763996573704)

正常情况下，如果需要删除 GitHub 上不需要的`repos`，手动删除的操作有点繁琐。如果只要删除一个还能接受，手动删除多个 repos 就有点浪费时间了。其实我们可以通过 GitHub 的 API 接口来批量删除不需要的`repos`。

1.  将要删除的`repos`按照`username\repos-name`的格式以一行一个存放到文本文件中。

![](https://user-gold-cdn.xitu.io/2019/1/19/1686546f8760a41a?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

2.  在 [GitHub](https://github.com/settings/tokens/new) 上申请具有删除`repos`权限的`token`。  
    
    ![](https://user-gold-cdn.xitu.io/2019/1/19/1686547d5319f0f5?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
    
3.  在命令行中运行下面的命令：
    

*   **Linux**

```
while read r;do curl -XDELETE -H 'Authorization: token xxx' "https://api.github.com/repos/$r ";done < repos
复制代码
```

*   **Windows**(PowerShell)

```
\[Net.ServicePointManager\]::SecurityProtocol = \[Net.SecurityProtocolType\]::Tls12
get-content D:\\repolist.txt | ForEach-Object { Invoke-WebRequest -Uri https://api.github.com/repos/$\_ -Method “DELETE” -Headers @{"Authorization"="token xxx"} }
复制代码
```