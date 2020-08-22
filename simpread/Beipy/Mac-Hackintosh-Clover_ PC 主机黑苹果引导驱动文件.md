\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[github.com\](https://github.com/Beipy/Mac-Hackintosh-Clover)

[![](https://github.com/Beipy/Mac-Hackintosh-Clover/raw/master/about/Mac.png)](https://github.com/Beipy/Mac-Hackintosh-Clover/blob/master/about/Mac.png)

[![](https://camo.githubusercontent.com/2a19ea539411f00882b13b3a97fea1e89cf316c3/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4d61634f532d31302e31332d2d3e31342d626c756576696f6c65742e737667)](https://camo.githubusercontent.com/2a19ea539411f00882b13b3a97fea1e89cf316c3/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4d61634f532d31302e31332d2d3e31342d626c756576696f6c65742e737667) [![](https://camo.githubusercontent.com/13680234a78db1b99f03e2f868f9739d62461476/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f417574686f722d42656970792d3030393366662e737667)](http://www.beipy.com/) 

### [](#吐槽)吐槽

花少钱体验顶配苹果，少花冤枉钱，追求极致黑苹果系统。技术不止，折腾不止。

为什么喜欢黑苹果，看列表对比! 没有对比没有伤害，价格伤害伤不起， 当然如果如果你是土豪或者苹果铁粉颜值控请关闭此页面。

以下对比皆以苹果官网最高配电脑对比:

<table><thead><tr><th>普通电脑</th><th>CPU</th><th>显卡</th><th>价格</th><th>优势</th><th>Mac 设备</th><th>CPU</th><th>显卡</th><th>价钱</th></tr></thead><tbody><tr><td>品牌笔记本</td><td>i5</td><td>核显</td><td>3k-4k</td><td>秒杀 &gt;</td><td>MacBook</td><td>i5</td><td><del>HD615</del></td><td><del>11867</del></td></tr><tr><td>品牌笔记本</td><td>i7</td><td>独显 4G</td><td>5k</td><td>秒杀 &gt;</td><td>MacBookAir</td><td><del>i5</del></td><td><del>UHD617</del></td><td><del>10812</del></td></tr><tr><td>品牌笔记本</td><td>i9</td><td>独显 6G</td><td>8k-15K</td><td>秒杀 &gt;</td><td>MacBook Pro</td><td>i9</td><td><del>560X 4G</del></td><td><del>21399</del></td></tr><tr><td>DIY 微主机</td><td>i5</td><td>独显 4G</td><td>3k-5K</td><td>秒杀 &gt;</td><td>Mac mini</td><td>i5</td><td><del>UHD630</del></td><td><del>8669</del></td></tr><tr><td>DIY 中配主机</td><td>i7</td><td>AMD 8G</td><td>5k</td><td>秒杀 &gt;</td><td>27 寸 iMac</td><td><del>i5</del></td><td>580X 8G</td><td><del>17728</del></td></tr><tr><td>DIY 主机</td><td>i9</td><td>AMD 11G</td><td>1W</td><td>秒杀 &gt;</td><td>iMac Pro</td><td>XeonW</td><td><del>Vega56 8G</del></td><td><del>38138</del></td></tr></tbody></table>

[](#正文描述)正文描述
-------------

从网上搜集了一些黑苹果 Clover 驱动配置文件，上传这些 Clover 驱动配置文件仅供大家参考使用，希望大家的黑苹果上少走一些弯路。

笔记本包括: Acer、LG、华为、华硕、小米、惠普、戴尔、机械革命、神舟、联想、雷神等品牌。

另外安装系统时候注意 10.14 版本以上不在支持 GTX 显卡，电脑默认有 N 卡的请安装 10.13 版本系统可以驱动 N 卡，部分 AMD 免驱。

> 通用安装步骤：[通用安装说明](https://github.com/Beipy/Mac-Hackintosh-Clover/blob/master/about/README.md) 通用安装步骤：[Other 插件说明](https://github.com/Beipy/Mac-Hackintosh-Clover/blob/master/Other/README.md) 部分插件可能偏老请，自行百度更新新插件。

如果你有其他已经解决的 Clover 驱动请直接投稿：\*\* [beipy0@163.com](mailto:beipy0@163.com) \*\*

[](#pc台式机)PC 台式机
----------------

<table><thead><tr><th>黑苹果常见台式机驱动 Clover 配置文件分享</th></tr></thead><tbody><tr><td>E3-1230 + 技嘉 P75D3+GTX650+10.13</td></tr><tr><td>E3-1230Ⅴ2+GTX470 + 华硕 p8b75v</td></tr><tr><td>E3-1231V3 + 华硕 B85+GTX1050Ti</td></tr><tr><td>E3-1245 + 华擎 B75+GTX760</td></tr><tr><td>E5-2680V2 + 华硕 P9+Quadro K4000+12.6</td></tr><tr><td>E5-2680V2 + 华南 X79V2+BIOS</td></tr><tr><td>EFI for Z370</td></tr><tr><td>G4560 + 华硕 B150M+10.13</td></tr><tr><td>H61-3570-650Ti-retal8111</td></tr><tr><td>i3-2120 - 华硕 P8H61-MLX Plus+GTX650+RTL8192CU+12.6</td></tr><tr><td>i3-4170 + 华硕 H81M+HD4600</td></tr><tr><td>i3-4330 + 华硕 H81T R2.0+HD4600</td></tr><tr><td>i3-7100 + 微星 H110+HD630+10.13</td></tr><tr><td>i3-8100 + 技嘉 B360M-GAMMING-HD+UHD630+10.13.5</td></tr><tr><td>i5-3470+B75M d2p+10.12.4</td></tr><tr><td>i5-4460 + 华硕 H81M-K</td></tr><tr><td>i5-4570 + 华硕 B85-E+GTX650-10.14</td></tr><tr><td>i5-4590 + 技嘉 B85+GTX970</td></tr><tr><td>i5-4590 + 华硕 B85M-G+HD4600+10.13</td></tr><tr><td>i5-4750 + 华硕 By85+GTX750</td></tr><tr><td>i5-6400 + 华硕 B150M-k D3+10,13</td></tr><tr><td>i5-6400 + 华硕 H110M-E+10.13</td></tr><tr><td>i5-6400 + 技嘉 H110M-S2+GTX750</td></tr><tr><td>i5-6500+B150M-WIND+GTX950</td></tr><tr><td>i5-6500+Z170+GTX1070+10.13</td></tr><tr><td>i5-6500 + 技嘉 B150-D3H+GTX950</td></tr><tr><td>i5-6500 + 技嘉 B150M-D3H+GTX1060+alc892+10.12.6</td></tr><tr><td>i5-6500 + 华硕 B250m-k+GT730+10.13</td></tr><tr><td>i5-6500 + 微星 H110M PRO VD-PLUS+GTX1050</td></tr><tr><td>i5-7500+B250+GTX1050TI</td></tr><tr><td>i5-7500+B250M+GTX1050</td></tr><tr><td>i5-7500 + 华硕 B250H+GTX1060</td></tr><tr><td>i5-7500 + 华硕 B250M PLUS+10.13</td></tr><tr><td>i5-7500 + 技嘉 B250m+GTX1050Ti+10.12.5</td></tr><tr><td>i5-7500 + 华硕 EX H110M V+GTX1060</td></tr><tr><td>i5-7500 + 七彩虹 B250m+GTX1070+10.13</td></tr><tr><td>i5-7600K + 技嘉 Z270X-UD3+GTX 1050</td></tr><tr><td>i5-8400+Z370N+10.13</td></tr><tr><td>i5-8400 + 技嘉 B360M D3SH</td></tr><tr><td>i5-8400 + 华硕 B360m+1050Ti</td></tr><tr><td>i5-8400 + 华硕 Z370-A+UHD630+10.13</td></tr><tr><td>i5-8400 + 华擎 z370Pro4+GTX1050</td></tr><tr><td>i5-8500 + 微星 B360M MORTAR+10.13.6</td></tr><tr><td>i5-8600k+MSI-Z370M-MORTAR+HD630</td></tr><tr><td>i5-8600k + 华硕 370F+GTX1050Ti</td></tr><tr><td>i7-4700_B85M-D3V</td></tr><tr><td>i7-4790 + 华硕 B85M-G+10.12+10.13</td></tr><tr><td>i7-4790K + 华硕 Z97-A+10.13+N 卡</td></tr><tr><td>i7-4790k+Z97-D3H</td></tr><tr><td>i7-6700+Z170+GTX1080</td></tr><tr><td>i7-6700+Z170+GTX970</td></tr><tr><td>i7-6700 + 华硕 B150M+GTX1050+10.13</td></tr><tr><td>i7-6700K + 技嘉 Z170+GTX760+10.13</td></tr><tr><td>i7-6700K + 华硕 Z170-P</td></tr><tr><td>i7-7700 + 华硕 B250+10.13</td></tr><tr><td>i7-7700+Dell-OptiPlex7050+HD630</td></tr><tr><td>i7-7700 + 技嘉 BM250+GTX1060</td></tr><tr><td>i7-7700K+GTX1080 + 华硕 Z270H</td></tr><tr><td>i7-7700K + 华硕 Z270+GTX1080</td></tr><tr><td>i7-7700k+Z270 主板的通用模版</td></tr><tr><td>i7-7700k + 华硕 PRIME Z270-P</td></tr><tr><td>i7-7700k + 华硕 Z270-A+NVme 硬盘</td></tr><tr><td>i7-8700 + 技嘉 Z370+GTX1060</td></tr><tr><td>i7-8700K+ASUS-370-E+UHD630</td></tr><tr><td>i7-8700K+MSIZ370-A+GTX1050Ti+10.13.4</td></tr><tr><td>i7-8700K+MSIZ370-A+GTX1060</td></tr><tr><td>i7-8700K+OC4.8+MSI Z370+itx 16G+GTX760</td></tr><tr><td>i7-8700K + 华硕 Z370-i+GTX1060+10.13.4</td></tr><tr><td>i7-8700K + 微星 z370M 终结者</td></tr><tr><td>i7-8700k+Z3700+1050Ti</td></tr><tr><td>技嘉 B150M</td></tr><tr><td>华硕 B150M-k d3+HD530+10.13.6</td></tr><tr><td>华硕 p8h61-m LX 主板</td></tr></tbody></table>

[](#acer宏碁笔记本)Acer 宏碁笔记本
------------------------

<table><thead><tr><th>Acer 笔记本黑苹果驱动配置文件分享</th></tr></thead><tbody><tr><td>Acer Aspire VN7-591G+i5-4210H</td></tr><tr><td>Acer E1-570</td></tr><tr><td>Acer E1-572G+i5-4200U+10.12</td></tr><tr><td>Acer E5 572G+i5-4200U+10.11</td></tr></tbody></table>

[](#lg笔记本)LG 笔记本
----------------

<table><thead><tr><th>LG 笔记本黑苹果驱动配置文件分享</th></tr></thead><tbody><tr><td>LG 15Z960</td></tr></tbody></table>

[](#华为笔记本)华为笔记本
---------------

<table><thead><tr><th>华为笔记本黑苹果驱动配置文件分享</th></tr></thead><tbody><tr><td>荣耀 Magic Book i+10.13.4</td></tr></tbody></table>

[](#华硕笔记本)华硕笔记本
---------------

<table><thead><tr><th>华硕笔记本黑苹果驱动配置文件分享</th></tr></thead><tbody><tr><td>华硕 FL5900+i7-7500U</td></tr><tr><td>华硕 FX50V+i5-6300HQ+HD530+ALC255+10.13</td></tr><tr><td>华硕飞行堡垒 FX53VD</td></tr><tr><td>华硕飞行堡垒 FX50VX+i5-6300HQ+10.12.4</td></tr><tr><td>华硕飞行堡垒 FXPRO6300(GL552VW)</td></tr></tbody></table>

[](#小米笔记本)小米笔记本
---------------

<table><thead><tr><th>小米笔记本黑苹果驱动配置文件分享</th></tr></thead><tbody><tr><td>小米 12.5 寸 1 代</td></tr><tr><td>小米 13.3-15.6+i7-8550U</td></tr><tr><td>小米 13.3 无指纹版</td></tr><tr><td>小米 15.6+i7-8550U</td></tr><tr><td>小米 Pro</td></tr><tr><td>小米 air 八代 i5 - 可休眠</td></tr><tr><td>小米 i5 指纹版 + 10.13.3</td></tr><tr><td>小米指纹版 - i5-7200U</td></tr></tbody></table>

[](#惠普笔记本)惠普笔记本
---------------

<table><thead><tr><th>惠普笔记本黑苹果驱动配置文件分享</th></tr></thead><tbody><tr><td>HP Elitebook 8 系列笔记本</td></tr><tr><td>惠普 Elitebook 1050 G1-i7 8750H-UHD630</td></tr><tr><td>惠普 envy x360 15bq+i5-8250U</td></tr><tr><td>光影精灵 + i5-6300HQ</td></tr><tr><td>暗影精灵 2 代 Pro+i7-7700HQ+UHD630+GTX1050</td></tr><tr><td>暗影精灵 3 电竞版 i5</td></tr><tr><td>惠普畅游人 i5-8250U+UHD620+alc295</td></tr><tr><td>惠普暗影精灵 2 i7-6700HQ+965M</td></tr></tbody></table>

[](#戴尔笔记本)戴尔笔记本
---------------

<table><thead><tr><th>戴尔笔记本黑苹果驱动配置文件分享</th></tr></thead><tbody><tr><td>Dell 15 5577+i5-7300HQ+HD630+GTX1050</td></tr><tr><td>Dell E6230+10.12.6</td></tr><tr><td>Dell Inspiron 7520</td></tr><tr><td>Dell Vostro 成就 5459+i7-6500U+10.12.5</td></tr><tr><td>Dell XPS 13 9350 i7-6500U+3k 触摸屏 + 10.13.6</td></tr><tr><td>Dell XPS 15 9550 i7-6700 适配 4K 和 1080+ 10.14.5</td></tr><tr><td>Dell 燃 7000</td></tr><tr><td>Dell 灵越 15 3543+i5-5200U</td></tr><tr><td>Dell 灵越 3567+i5-7200</td></tr><tr><td>Dell 游匣 7577+i7-7700HQ</td></tr><tr><td>Dell7420 i7 完美</td></tr></tbody></table><table><thead><tr><th>机械革命笔记本黑苹果驱动配置文件分享</th></tr></thead><tbody><tr><td>机械革命 - 深海泰坦 X1+i5-7300</td></tr><tr><td>机械革命 S1+i5-8250U+MX150</td></tr><tr><td>机械革命 X6M</td></tr><tr><td>机械革命 X6TI-S i7-6700HQ+960M+10.13</td></tr><tr><td>机械革命 X6Ti-S+i7-7700HQ+GTX1050Ti</td></tr><tr><td>机械革命 X7TI-S+i7-6700HQ+GTX1050+10.13</td></tr></tbody></table>

[](#海尔笔记本)海尔笔记本
---------------

<table><thead><tr><th>海尔笔记本黑苹果驱动配置文件分享</th></tr></thead><tbody><tr><td>海尔 X3-pro i5-4210</td></tr></tbody></table>

[](#神舟笔记本)神舟笔记本
---------------

<table><thead><tr><th>神舟笔记本黑苹果驱动配置文件分享</th></tr></thead></table>

| 神舟 Z7 + 蓝天 P650SE+4K 屏 + 10.12 | | 神舟 K590S+i7-3612QM+HD4000+GTX660+10.13 | | 炫龙阿尔法 N650DU+i5-8400+UHD630 |

[](#联想笔记本)联想笔记本
---------------

[](#雷神笔记本)雷神笔记本
---------------

<table><thead><tr><th>雷神笔记本黑苹果驱动配置文件分享</th></tr></thead><tbody><tr><td>雷神 911</td></tr></tbody></table>

[](#微星笔记本)微星笔记本
---------------

<table><thead><tr><th>微星笔记本黑苹果驱动配置文件分享</th></tr></thead><tbody><tr><td>微星 GE40 2PC-486XCN+i5-4210M+HD4600+GTX850M+ALC269</td></tr></tbody></table>

[](#打赏)打赏
---------

* * *

*   \*\* 支持项目继续完善下去，你也可以贡献一份力量！💰打赏，更会有更新的动力
*   `也可以支付宝扫码红包来赠送微薄之力！` [![](https://raw.githubusercontent.com/Beipy/VipVideoResolution/master/img/TestImg/dashang.png)](https://raw.githubusercontent.com/Beipy/VipVideoResolution/master/img/TestImg/dashang.png)

[](#日志)日志
---------

#### [](#2020-02-24)`2020-02-24`

*   更新驱动 Dell XPS 15 9550 i7-6700 适配 4K 和 1080+ 10.15.3

#### [](#2019-07-03)`2019-07-03`

*   新增微台式机 i7-7700+Dell-OptiPlex7050+HD630 ；
*   新增 i5-7500 + 技嘉 B250-D3H +GTX1050

#### [](#2019-07-30)`2019-07-30`

*   Dell XPS 15 9550 i7-6700 适配 4K 和 1080+ 10.14.5