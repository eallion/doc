\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[conversun.com\](https://conversun.com/2019/08/19/OpenClash-SmartDns/)

[](#设备 "设备")设备
--------------

*   CPU: Intel 3205U
*   RAM: 8G DDR3 1600
*   SSD: 64G
*   HDD: 1T

[![](https://img.conversun.com/images/20201710251-KLm7NW.png!jpg)](https://img.conversun.com/images/20201710251-KLm7NW.png!jpg)

### [](#URL-Test-正常 "URL-Test 正常")URL-Test 正常

[![](https://img.conversun.com/images/20191226111714-KU7zop.jpg!jpg)](https://img.conversun.com/images/20191226111714-KU7zop.jpg!jpg)

### [](#分流效果 "分流效果")分流效果

#### [](#Netflix "Netflix")Netflix

[![](https://img.conversun.com/images/20191226111856-YFyvgn.jpg!jpg)](https://img.conversun.com/images/20191226111856-YFyvgn.jpg!jpg)

#### [](#Baidu "Baidu")Baidu

[![](https://img.conversun.com/images/20191226111929-vC0AFt.jpg!jpg)](https://img.conversun.com/images/20191226111929-vC0AFt.jpg!jpg)

[](#资源 "资源")资源
--------------

本文所用文件, 于路由访问 Github 过慢时使用, 可直接 wget 下载

**Openwrt 镜像**

推荐固件, 自带 Openclash, SmartDNS(已配置好):

[x86\_64 clashOpenWRT 软路由固件频道](https://t.me/clashOpenWRT233)

CDN:  
[openwrt-x86-64-generic-squashfs-combined.img.gz](https://img.conversun.com/files/openwrt/openwrt-x86-64-generic-squashfs-combined.img.gz)

**OpenClash**

[luci-app-openclash-beta\_all.ipk](https://img.conversun.com/files/openwrt/luci-app-openclash-beta_all.ipk)  
[clash](https://img.conversun.com/files/openwrt/clash)

**SmartDns**

[smartdns.1.2019.06.21-2337.x86\_64-openwrt-all.ipk](https://img.conversun.com/files/openwrt/smartdns.1.2019.11.02-1102.x86_64-openwrt-all.ipk)  
[smartdns.luci-app-smartdns.1.2019.11.02-1102.all-luci-all.ipk](https://img.conversun.com/files/openwrt/smartdns.luci-app-smartdns.1.2019.11.02-1102.all-luci-all.ipk)

**相关文档**

[OpenClash Wiki](https://github.com/vernesong/OpenClash/wiki)  
[SmartDNS 配置](https://github.com/pymumu/smartdns#openwrtlede)

[](#安装 "安装")安装
--------------

### [](#软路由刷入 "软路由刷入")软路由刷入

教程较多, 这里不做阐述, 参考:

[空盘软路由安装](https://medium.com/@muchenran2/%E7%A9%BA%E7%9B%98%E8%BD%AF%E8%B7%AF%E7%94%B1%E5%AE%89%E8%A3%85-lede-61e419301368)  
[iKuai 视频教程](https://www.ikuai8.com/?view=article&id=527&type=gw)

### [](#OpenClash-安装 "OpenClash 安装")OpenClash 安装

设置 Wan/Lan 口, 拨号上网等, SSH 到路由

```
cd ~
wget https://img.conversun.com/files/openwrt/luci-app-openclash-beta\_all.ipk
wget https://img.conversun.com/files/openwrt/clash
opkg install luci-app-openclash-beta\_all.ipk
mv clash /etc/openclash/core/clash
cd /etc/openclash
chmod 0755 clash
```

### [](#SmartDNS "SmartDNS")SmartDNS

```
cd ~
wget https://img.conversun.com/files/openwrt/smartdns.1.2019.11.02-1102.x86\_64-openwrt-all.ipk
wget https://img.conversun.com/files/openwrt/smartdns.luci-app-smartdns.1.2019.11.02-1102.all-luci-all.ipk
opkg install smartdns.1.2019.06.21-2337.x86\_64-openwrt-all.ipk
opkg install smartdns.luci-app-smartdns.1.2019.11.02-1102.all-luci-all.ipk
```

[](#配置 "配置")配置
--------------

### [](#OpenClash "OpenClash")OpenClash

#### [](#全局设置 "全局设置")全局设置

建议使用 Fake IP

[![](https://img.conversun.com/images/202017102430-tUFrIj.png!jpg)](https://img.conversun.com/images/202017102430-tUFrIj.png!jpg)

#### [](#DNS "DNS")DNS

上游 DNS 搭配 SmartDNS 时再修改

[![](https://img.conversun.com/images/202017102546-BaIR0i.png!jpg)](https://img.conversun.com/images/202017102546-BaIR0i.png!jpg)

#### [](#规则设置 "规则设置")规则设置

*   ~lhie1 的机场托管中的规则不适合路由器, 这里桥接成了 [ConnersHua](https://github.com/ConnersHua/Profiles) 的规则~
*   可选桥接其他规则 (控制面板选项不变)

[![](https://img.conversun.com/images/202017103218-TRKOQm.png!jpg)](https://img.conversun.com/images/202017103218-TRKOQm.png!jpg)

#### [](#配置订阅 "配置订阅")配置订阅

DlerCloud 除了订阅之外自带了主流应用的托管, clash, surge 等

AFF 链接 [dlercloud.co](https://dlercloud.co/auth/register?affid=28996)  
[![](https://img.conversun.com/images/202017103443-VnYx3v.png!jpg)](https://img.conversun.com/images/202017103443-VnYx3v.png!jpg)

#### [](#版本更新 "版本更新")版本更新

最新版本的 OpenClash 处于 Fake IP 模式下并正常联通时, 此处更新将通过代理下载, 解决从 Github 更新失败问题

首次下载内核困难可使用 CDN 下载

```
cd ~
wget https://img.conversun.com/files/openwrt/clash
mv clash /etc/openclash/clash
cd /etc/openclash
chmod 0755 clash
```

[![](https://img.conversun.com/images/202017103512-MUeOeH.png!jpg)](https://img.conversun.com/images/202017103512-MUeOeH.png!jpg)

### [](#SmartDNS-1 "SmartDNS")SmartDNS

#### [](#配置-1 "配置")配置

##### [](#基本设置 "基本设置")基本设置

其中本地端口按需填写

[![](https://img.conversun.com/images/202017101251-3o4AiL.png!jpg)](https://img.conversun.com/images/202017101251-3o4AiL.png!jpg)

##### [](#上游服务器 "上游服务器")上游服务器

**公共 DNS 参考**

*   [https://www.ip.cn/dns.html](https://www.ip.cn/dns.html)
*   [https://dns.icoa.cn](https://dns.icoa.cn/)

[![](https://img.conversun.com/images/20201710163-dwixIS.png!jpg)](https://img.conversun.com/images/20201710163-dwixIS.png!jpg)

##### [](#其他说明 "其他说明")其他说明

*   若使用 OpenClash 的 Fake-IP 模式, 仅国内的解析会走 SmartDNS
*   污染严重地区可尝试 tls 协议 DNS

#### [](#作为-OpenClash-上游 "作为 OpenClash 上游")作为 OpenClash 上游

设置为 SmartDNS 端口即可

[![](https://img.conversun.com/images/202017102333-eRDtWu.png!jpg)](https://img.conversun.com/images/202017102333-eRDtWu.png!jpg)