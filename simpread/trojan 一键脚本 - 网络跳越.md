\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[hijk.art\](https://hijk.art/trojan-one-click-scrip/)

> 使用过程中遇到问题，欢迎到 [网络跳越论坛](https://hijk.club/) 或 tg 群组 [https://t.me/hijkclub](https://t.me/hijkclub) 交流

如果你这周看到本站默默地在更新 trojan 客户端教程，是不是想到服务端一键脚本也快了？没错，今天正式完成了 trojan 一键安装脚本，支持 CentOS 7/8 和 Ubuntu 16.04 及以上版本，目前已经上传到 [Github](https://github.com/hijkpw/scripts)。

**提示：**这是自己搭建科学上网环境的第三步，请确认已经做了前两步：

1.  购买服务器和域名。想服务器速度快请参考 [搬瓦工 VPS 购买教程](https://hijk.art/bandwagonghost-buy-vps-tutorial/) 或  [购买 AkkoCloud 德国、美西 CN2 GIA VPS](https://www.akkocloud.com/aff.php?aff=122&gid=7) ，想 ip 被封后免费换请参考：[购买 vultr 服务器超详细图文教程](https://hijk.art/vultr-buy-vps-tutorial/)，购买域名可参考：[Namesilo 购买域名详细教程](https://hijk.art/namesilo-buy-domain-tutorial/)；
2.  连接到服务器。Windows 系统请参考 [Bitvise 连接 Linux 服务器教程](https://hijk.art/bitvise-connect-linux-server-tutorial/)，mac 用户请参考 [Mac 电脑连接 Linux 教程](https://hijk.art/mac-connect-to-linux-tutorial/)。

**注意：**

1\. 如果服务器已经有运行网站，请联系网站运维再执行脚本，否则可能导致原来网站无法访问，本人不负责！

2\. 对域名没有要求，不管国内还是国外注册的都可以，**不需要备案**，不会影响使用，也不会带来安全 / 隐私上的问题；

3\. 根据 [Namesilo 购买域名详细教程](https://hijk.art/namesilo-buy-domain-tutorial/) 购买的域名，默认 @和 www 在买之前都已经做了解析，因此尽管 www 已经改成了你服务器的 ip，但执行本脚本时可能还会出现 “主机未解析到当前服务器 IP” 的错误。这时只需要换个名称做解析即可，例如 www2；

4\. 除非 443 端口被墙或另有它用，建议使用 443！

5\. 如果想上 cdn，请根据本教程操作完后再参考：**[使用 cloudflare 中转流量，拯救被墙 ip](https://hijk.art/use-cloudflare-unlock-blocked-ip/)；**

6\. BBR 换成魔改 BBR/BBR Plus / 锐速清参考**：[安装魔改 BBR/BBR Plus / 锐速 (Lotserver)](https://hijk.art/install-bbr-plus-lotserver/)；**

7\. **本脚本请勿与 [v2ray 带伪装一键脚本](https://hijk.art/v2ray-one-click-script-with-mask/) 在同一个 vps 上运行，除非你能手动解决冲突！**

8\. 刚搭建好 trojan 不要猛上流量，否则可能导致被限速、端口被墙，严重可能 ip 被墙。

使用教程
----

1\. 如果 vps 运营商开启了防火墙（阿里云、google 云等默认开启，搬瓦工 / hostdare/vultr 默认放行所有端口），请先登录 vps 管理后台放行 80 和 443 端口，否则会导致获取证书失败；

2\. 登录到服务器（windows 请参考 [Bitvise 连接 Linux 服务器教程](https://hijk.art/bitvise-connect-linux-server-tutorial/)，mac 用户请参考 [Mac 电脑连接 Linux 教程](https://hijk.art/mac-connect-to-linux-tutorial/)），在终端（黑框框）输入如下命令：

```
bash <(curl -sL https://raw.githubusercontent.com/hijkpw/scripts/master/trojan.sh)
```

按回车键，屏幕上开始滚动各种看得懂看不懂的东西。紧盯着屏幕，直到屏幕出现 “**确认满足按 y，按其他退出脚本：**”，确认条件满足，按 y，回车，然后**输入你域名的主机名**（注意是主机名，比如 hijk.art，**不建议填裸域名** hijk.pw！），密码、端口（建议用默认的 443！）和选择是否安装 BBR。

接下来脚本会自动疯狂运行，**如果安装过程卡住，请耐心等待几分钟；**期间网络断开（windows 上表现为黑框框中或者顶部标题出现 disconnected 字样，mac 表现为终端出现 “closed by remote host” 或”broken pipe”），请重新连接后再次执行命令。脚本运行成功会输出配置信息，截图如下：

[![](https://hijk.art/wp-content/uploads/2020/03/trojan一键脚本输出结果.png)](https://hijk.art/wp-content/uploads/2020/03/trojan%E4%B8%80%E9%94%AE%E8%84%9A%E6%9C%AC%E8%BE%93%E5%87%BA%E7%BB%93%E6%9E%9C.png)

trojan 一键脚本输出结果

**到此服务端配置完毕**，服务器可能会自动重启（**没提示重启则不需要**），windows 终端出现 “disconnected”，mac 出现“closed by remote host” 说明服务器成功重启了。

可能出现的问题
-------

1\. 多次运行一键脚本，安装过程中会出现如下提示：

```
What would you like to do?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: Keep the existing certificate for now
2: Renew & replace the cert (limit ~5 per 7 days)
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate number \[1-2\] then \[enter\] (press 'c' to cancel):

```

**输入 1，回车即可。**

2\. 如果提示证书失败，终端出现如下提示：

```
An unexpected error occurred:
There were too many requests of a given type :: Error creating new order :: too many certificates already issued for exact set of domains:test2.hijk.pw: see https://letsencrypt.org/docs/rate-limits/

```

说明这个主机名近期申请过太多次免费证书，请换一个主机名尝试，例如 test2.hijk.pw 换成 test3.hijk.pw（需要到 dns 控制台添加解析）。

客户端下载
-----

接下来是**科学上网最后一步**：

1\. 下载  [trojan 客户端](https://hijk.art/trojan-clients/)；

2\. 配置客户端：windows 请参考 [Windows trojan 客户端配置教程](https://hijk.art/trojan-windows-client-tutorial/)，mac 请参考 [trojan mac 客户端配置教程](https://hijk.art/trojan-mac-client-config-tutorial/)，安卓请参考 [trojan 安卓客户端配置教程](https://hijk.art/trojan-android-client-config-tutorial/)，iOS 请参考 [Shadowrocket 配置 trojan 教程](https://hijk.art/shadowrocket-config-trojan-tutorial/)。

一切顺利的话，就可以愉快的上外网了！

其他
--

1\. 查看 trojan 运行状态 / 配置：`bash <(curl -sL https://raw.githubusercontent.com/hijkpw/scripts/master/trojan.sh) info`

2\. trojan 管理命令：启动：`systemctl start trojan`，停止：`systemctl stop trojan`，重启：`systemctl restart trojan`；

3\. 更新 trojan 到最新版：`bash -c "$(curl -fsSL https://raw.githubusercontent.com/trojan-gfw/trojan-quickstart/master/trojan-quickstart.sh)"`

4\. 查看 SSL 证书：`certbot certificates`，更新证书：`systemctl stop nginx; certbot renew; systemctl restart nginx`

5\. 卸载： `bash <(curl -sL https://raw.githubusercontent.com/hijkpw/scripts/master/trojan.sh) uninstall`

参考
--

1\. [trojan 教程](https://tlanyan.me/trojan-tutorial/)

文章最后修改日期：2020 年 6 月 20 日