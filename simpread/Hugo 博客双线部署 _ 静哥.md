\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[linsage.com\](https://linsage.com/posts/hugo-coding-netlify/)

![](https://linsage.com/svg/loading.small.min.svg)

Hugo 是由 Go 语言实现的静态网站生成器。简单、高效、快速部署，可以自定义使用各种开源主题，本站采用 LoveIt。

静态网站托管，考虑到国内、国外的差异，可选用不同的静态网站托管服务，国内 Coding.net，国外有 Netlify、GitHub，都提供了免费的托管服务及构建服务，通过域名解析，根据 ip 来源实现 dns 解析访问。

*   Coding.net
*   Github

git 提交代码推送，调整. git 配置 config 文件，实现 push 同时推送到分两个仓库

发布库 = 静态网站资源

*   Coding.net：定义**发布库**（区别于源代码库，方便管理和部署）并开启静态网站服务
*   Github：定义 xxx.github.io 来实现托管
*   Netlify：提供直接托管

主机位置：新加坡 腾讯云

![](https://linsage.com/svg/loading.small.min.svg)

基于 Jenkinsfile，基于 docker 环境，公开镜像库，[https://hub.docker.com/](https://hub.docker.com/r/monachus/hugo)

发布库项目令牌：项目 - 开发者选项 - 定义

参考如下

```
\[remote "origin"\]
    url = https://github.com/linsage/blog.git
    url = https://e.coding.net/linsage/blog.git
```

![](https://linsage.com/svg/loading.small.min.svg)

主机位置：新加坡 digitalocean

配置相当简单，界面化配置，配置 hugo 环境及触发条件即可

![](https://linsage.com/svg/loading.small.min.svg)

![](https://linsage.com/svg/loading.small.min.svg)

效果：[https://linsage.com](https://linsage.com/)

根据访问者 ip 的来源，通过 dns 解析线路实现

![](https://linsage.com/svg/loading.small.min.svg)

![](https://linsage.com/svg/loading.small.min.svg)