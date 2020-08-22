\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[koolshare.cn\](https://koolshare.cn/thread-153015-1-1.html)  ![](https://koolshare.cn/uc_server/avatar.php?uid=219300&size=middle) bryant2 _ 本帖最后由 bryant2 于 2020-4-25 12:59 编辑_  
**引言**  
前不久把家里电信光纤升级到了 199 的 300M 套餐（其实当时是为了无限流量卡，因为工作需要经常出差，有一个插 SIM 卡的随身华为路由器）。升级到 300M 之后，直接光猫测速是可以跑满，接上路由器之后，就依旧停留在 200M + 的速度…  
首先想到先换路由，某东看了一晚，又看了一些媒体文章，下手 Linksys Velop AC2600 Mesh 分布式，速度 OK 了。但又来一个问题，目前 Mesh 路由貌似普遍都不支持 OpenWrt / LEDE 第三方固件，毕竟原厂固件还是有其定制功能和硬件优化的优势。  
  
  
**软路由**  
之前的路由是 NetGear WNDR4300 ，经典爆款！玩了几年的 OpenWrt / LEDE , 所以轻车熟路，从下单到收货，晚上 2 个小时搞定安装配置。某宝找的 j1900 ， 4 千兆口（Intel i211AT），直接上图  
  
![](https://image.koolshare.cn/attachment/forum/201812/27/171053cciorc3rv9oi37qe.jpg)

**1.jpg** _(178.58 KB, 下载次数: 57)_

[下载附件](forum.php?mod=attachment&aid=MjczMzAwfGM5N2JhNjg0fDE1OTgxMTEwODN8MHwxNTMwMTU%3D&nothumb=yes)

2018-12-27 17:10 上传

  
做工蛮好磨具精准整体颜值也还可以  
![](https://koolshare.cn/static/image/common/none.gif)

**2.jpg** _(313.04 KB, 下载次数: 6)_

[下载附件](forum.php?mod=attachment&aid=MjczMzAxfGE5NzYzODQ5fDE1OTgxMTEwODN8MHwxNTMwMTU%3D&nothumb=yes)

2018-12-27 17:13 上传

  
2G DDR3L 内存 + 16G mSata SSD （至于什么牌子的不关心了，毕竟现在还在生产这种容量的大厂几乎没有了吧，要么拆机货要么华强北货）  
可见大大的铝制散热片，靠散热硅脂与外壳贴合，达到外壳也可以传导热量作用。  
![](https://koolshare.cn/static/image/common/none.gif)

**3.jpg** _(225.1 KB, 下载次数: 5)_

[下载附件](forum.php?mod=attachment&aid=MjczMzAyfDY4ZjlkZGY1fDE1OTgxMTEwODN8MHwxNTMwMTU%3D&nothumb=yes)

2018-12-27 17:17 上传

  
4 个千兆 Intel i211 网卡 + 1 个 COM 口 + 2 个 USB2.0 ；另外一面只有 1 个 VGA + 12V5A 电源  
再次懵逼，DELL 2515H 没有 VGA 口 ！咋办？在业主群三更半夜找邻居家借显示器么? NO，**直接后台盲刷！**  
咨询卖家已刷 Koolshare 固件，那默认 DHCP 就应该开启了，LAN1 为 WAN 口，那 LAN2-4 就是 LAN 口；网线直连，ping 192.168.1.1 -t 可以响应，开 chrome 访问  192.168.1.1 访问 koolshare 固件的 Luci 图形化管理界面登录，OK，现在去 openwrt 官网找固件  
![](https://koolshare.cn/static/image/common/none.gif)

**openwrt.PNG** _(79.58 KB, 下载次数: 11)_

[下载附件](forum.php?mod=attachment&aid=MjczMzAzfDM1ZmI1YTg2fDE1OTgxMTEwODN8MHwxNTMwMTU%3D&nothumb=yes)

2018-12-27 17:28 上传

  
LEDE 其实是原来的 OpenWrt 组织分出去的，嫌弃 OP 管理混乱更新缓慢等等，不过今年初官宣又合并了，所以 LEDE 的最后版本停留在 17.01.6；而 OpenWrt 最新的版本为 **18.06.2** ; 内核升级支持软硬 NAT 等等，要刷肯定最新的稳定分支版本。此路径下找到 x86 64 的升级包  
![](https://koolshare.cn/static/image/common/none.gif)

**openwrt2.PNG** _(113.2 KB, 下载次数: 11)_

[下载附件](forum.php?mod=attachment&aid=MjczMzA0fDczM2U5ZGQ5fDE1OTgxMTEwODN8MHwxNTMwMTU%3D&nothumb=yes)

2018-12-27 17:33 上传

  
下载红线的这个，第一个是用于往 SSD 写镜像的文件，因为我是从 koolshare 后台去替换固件，所以选择第二个。至于为什么敢这样操作? 看了 koolshare 后台后我敢肯定核心还是 openwrt/lede ，只是自己的界面主题以及编译集成了数不清的插件程序，并做了深度的优化和定制（其实功能真的很强大，只是我喜欢简单的东西， LESS IS MORE）。  
下载好后直接去 koolshare 后台固件升级，等吧~ 其实此时心里忐忑，万一刷崩了，我又不能接显示器，看不到错误信息  
因为要 ping 路由我才好判断是否刷固件成功，先改网卡设置  
![](https://koolshare.cn/static/image/common/none.gif)

**网卡设置. PNG** _(108.26 KB, 下载次数: 9)_

[下载附件](forum.php?mod=attachment&aid=MjczMzA2fDBlNTM0YjE2fDE1OTgxMTEwODN8MHwxNTMwMTU%3D&nothumb=yes)

2018-12-27 17:42 上传

  
然后 ping 192.168.1.1 -t  
![](https://koolshare.cn/static/image/common/none.gif)

**ping.PNG** _(19.54 KB, 下载次数: 4)_

[下载附件](forum.php?mod=attachment&aid=MjczMzA3fDcxNWUyODgzfDE1OTgxMTEwODN8MHwxNTMwMTU%3D&nothumb=yes)

2018-12-27 17:43 上传

  
尼玛，还真不通，莫非刷成砖了… 别急，是不是网口变了，ping 界面开着，网线换口挨个捅它，把 LAN 网线从 2 号口换到了 1 号口，通了！说明 OpenWrt 刷完，之前 koolshare 下的 WAN 口现在变成了 LAN 口。登录吧~  
![](https://koolshare.cn/static/image/common/none.gif)

**wrt-1.PNG** _(35.9 KB, 下载次数: 4)_

[下载附件](forum.php?mod=attachment&aid=MjczMzEwfDkwMjBkNjhmfDE1OTgxMTEwODN8MHwxNTMwMTU%3D&nothumb=yes)

2018-12-27 17:47 上传

  
进去第一件事，网口绑定设置，将软路由 234 号口设置为 LAN，1 口设置为 WAN，保存并应用，Luci 界面里直接重启，网线换回到 2 口即可  
![](https://koolshare.cn/static/image/common/none.gif)

**ert-2.PNG** _(83.87 KB, 下载次数: 4)_

[下载附件](forum.php?mod=attachment&aid=MjczMzExfGU0N2E0ZDAwfDE1OTgxMTEwODN8MHwxNTMwMTU%3D&nothumb=yes)

2018-12-27 17:49 上传

  
接下来，因为要安装不可描述的插件，openWrt 的官方源国内连接很慢，所以换成国内镜像  
教育网国内源镜像，每天同步一次，更新及时！作废！  
  
update 20190705:  
目前来看，清华大学的开源镜像最稳定最快，推荐！将域名部分替换为：[mirrors.tuna.tsinghua.edu.cn/lede/](https://mirrors.tuna.tsinghua.edu.cn/lede/)  
![](https://koolshare.cn/static/image/common/none.gif)

**wrt-3.PNG** _(79.69 KB, 下载次数: 7)_

[下载附件](forum.php?mod=attachment&aid=MjczMzEyfGEyNDBkNmU3fDE1OTgxMTEwODN8MHwxNTMwMTU%3D&nothumb=yes)

2018-12-27 17:53 上传

  
替换域名这一段即可~ 用 PUTTY SSH 登录到路由器，安装不可描述部分省略 1000 字……  
![](https://koolshare.cn/static/image/common/none.gif)

**wrt-4.PNG** _(76.15 KB, 下载次数: 6)_

[下载附件](forum.php?mod=attachment&aid=MjczMzE0fGY3NDI4Nzc5fDE1OTgxMTEwODN8MHwxNTMwMTU%3D&nothumb=yes)

2018-12-27 17:55 上传

  
搞定！  
对了，差点忘了，原版的 OpenWrt 18.06.1 已经在 防火墙设置里，提供了 软 NAT 和 硬 NAT 开关，我分别尝试过，因为 j1900 不支持硬件 NAT，所以只开个软的就行啦  
![](https://koolshare.cn/static/image/common/none.gif)

**wrt-5.PNG** _(77.36 KB, 下载次数: 8)_

[下载附件](forum.php?mod=attachment&aid=MjczMzE2fGY4NTVhZjgxfDE1OTgxMTEwODN8MHwxNTMwMTU%3D&nothumb=yes)

2018-12-27 17:58 上传

  
实测不可描述部分的 NAT 转发，忽略掉我自己服务器的自身带宽瓶颈，不开之前，油管是 6-7W 左右，开了后最高是 9W ~  
稍后补图，截图在 ubuntu 系统下  
![](https://koolshare.cn/static/image/common/none.gif)

**Screenshot-from-2018-12-26-19-56-33.jpg** _(130.89 KB, 下载次数: 7)_

[下载附件](forum.php?mod=attachment&aid=MjczMzE4fDg2ZTg1ZTZifDE1OTgxMTEwODN8MHwxNTMwMTU%3D&nothumb=yes)

2018-12-27 18:35 上传

  
![](https://koolshare.cn/static/image/common/none.gif)

**Screenshot-from-2018-12-26-20-17-36.jpg** _(200.62 KB, 下载次数: 6)_

[下载附件](forum.php?mod=attachment&aid=MjczMzE5fGFkODA2NTQ3fDE1OTgxMTEwODN8MHwxNTMwMTU%3D&nothumb=yes)

2018-12-27 18:35 上传

  
![](https://koolshare.cn/static/image/common/none.gif)

**捕获. PNG** _(102.17 KB, 下载次数: 2)_

[下载附件](forum.php?mod=attachment&aid=Mzc0Nzc2fDFiNjFlMTY2fDE1OTgxMTEwODN8MHwxNTMwMTU%3D&nothumb=yes)

2020-4-25 12:57 上传

  
**总结**  
j1900 并不弱，关键还是看你的应用场景  
针对我这种，只需要路由功能 + 不可描述插件 + 自备 AP，起到全屋畅游并且跑满带宽的，j1900 足够；2020 年 3 月已升到 1000M，j1900 是完全可以应付的。所以，性价比，N2600 400 大洋，j1900 700 , 新入坑的坛友们自己权衡。  
  
  
![](https://koolshare.cn/uc_server/avatar.php?uid=60584&size=middle)xgcn  有动手能力，熟悉 linux 操作的话，搞定 openwrt 还是比较容易滴！![](https://koolshare.cn/uc_server/avatar.php?uid=155317&size=middle)natyou  我的 j1800 都跑得稳稳的 ![](https://koolshare.cn/uc_server/avatar.php?uid=192966&size=middle) aymayi 佩服厉害学习了 ![](https://koolshare.cn/uc_server/avatar.php?uid=1270&size=middle) fongnaxing 请问你的人 ubuntu 是 18.04 的吗? 有你这个版本的下载链接吗，感觉挺漂亮的 ![](https://koolshare.cn/uc_server/avatar.php?uid=43108&size=middle) Bobbiz 我记得 J1900 好像跑不满千兆的 600M 是极限了 ![](https://koolshare.cn/uc_server/avatar.php?uid=84147&size=middle) dvquest 

> [Bobbiz 发表于 2018-12-27 23:44](https://koolshare.cn/forum.php?mod=redirect&goto=findpost&pid=1730282&ptid=153015)  
> 我记得 J1900 好像跑不满千兆的 600M 是极限了

不好意思，你记错了。J1900 装的 2.19 实测千兆跑满没问题。![](https://koolshare.cn/uc_server/avatar.php?uid=180581&size=middle)dengleon  Ubuntu 是什么版本？按住到哪里呢？求个教程。  
佩服盲装。![](https://koolshare.cn/uc_server/avatar.php?uid=24128&size=middle)abull  这个算溜的 ![](https://koolshare.cn/uc_server/avatar.php?uid=7545&size=middle) tanken 

> [fongnaxing 发表于 2018-12-27 23:37](https://koolshare.cn/forum.php?mod=redirect&goto=findpost&pid=1730278&ptid=153015)  
> 请问你的人 ubuntu 是 18.04 的吗? 有你这个版本的下载链接吗，感觉挺漂亮的

官网或者其他地方到处都有还伸手啊？![](https://koolshare.cn/uc_server/avatar.php?uid=219300&size=middle)bryant2  _ 本帖最后由 bryant2 于 2018-12-28 12:12 编辑_  

> [fongnaxing 发表于 2018-12-27 23:37](https://koolshare.cn/forum.php?mod=redirect&goto=findpost&pid=1730278&ptid=153015)  
> 请问你的人 ubuntu 是 18.04 的吗? 有你这个版本的下载链接吗，感觉挺漂亮的

对的，借你的楼层回复  
我的 Ubuntu 就是原生的 18.04.1LTS ，千万不要以为我做了什么深度的美化和增强，一丁点都不复杂！  
其实就额外装了 2 个组件  
1> Gnome-tweak-tool  
18.04 的图形化界面是 Gnome ，其实它本来就有个设置工具叫 gnome-tweak-tool ，只要 apt-get update 一下，再  apt-get install gnome-tweak-tool 就有了  
2 > dash to dock  
就是下面图标的 dock 菜单栏，直接 18.04 的软件中心里面就有，装好了根据自己喜好配置一下  
3> 替换图标  
外有个著名的设计师为 ubuntu / debian 等 linux 系统设计了一套扁平化图标，就是我用的这个，装好后，还是用 gnome-tweak-tool 改下默认设置即可。  
网址： snwh 点 org  
![](https://koolshare.cn/static/image/common/none.gif)

**2.PNG** _(33.71 KB, 下载次数: 6)_

[下载附件](forum.php?mod=attachment&aid=MjczMzY4fDgzMmE5YmFhfDE1OTgxMTEwODN8MHwxNTMwMTU%3D&nothumb=yes)

2018-12-28 11:42 上传

  
![](https://koolshare.cn/uc_server/avatar.php?uid=1270&size=middle)fongnaxing  谢谢 po 耐心解答 ![](https://koolshare.cn/uc_server/avatar.php?uid=152111&size=middle) starttimes 前几天淘了个 289 块的 j1900，双 i211 网卡，4g 板结内存，8g ssd，带机箱电源，没上盖，今天能到，试试怎么样 ![](https://koolshare.cn/uc_server/avatar.php?uid=219300&size=middle) bryant2 

> [starttimes 发表于 2018-12-28 12:56](https://koolshare.cn/forum.php?mod=redirect&goto=findpost&pid=1730668&ptid=153015)  
> 前几天淘了个 289 块的 j1900，双 i211 网卡，4g 板结内存，8g ssd，带机箱电源，没上盖，今天能到，试试怎么样 ...

你这个性价比好高啊！只要硬件 OK，我想都不会有问题的 ![](https://koolshare.cn/uc_server/avatar.php?uid=198716&size=middle) m1484232791 膜拜大佬  虽然看不懂 但是还是感谢了 ![](https://koolshare.cn/uc_server/avatar.php?uid=165691&size=middle) zhangfeideya > [starttimes 发表于 2018-12-28 12:56](https://koolshare.cn/forum.php?mod=redirect&goto=findpost&pid=1730668&ptid=153015)  
> 前几天淘了个 289 块的 j1900，双 i211 网卡，4g 板结内存，8g ssd，带机箱电源，没上盖，今天能到，试试怎么样 ...

人品大爆发 ![](https://koolshare.cn/uc_server/avatar.php?uid=152111&size=middle)starttimes 

> zhangfeideya 发表于 2018-12-28 22:13  
> 人品大爆发

现在闲鱼上还有卖 ![](https://koolshare.cn/uc_server/avatar.php?uid=165691&size=middle) zhangfeideya 

> [starttimes 发表于 2018-12-28 23:03](https://koolshare.cn/forum.php?mod=redirect&goto=findpost&pid=1731395&ptid=153015)  
> 现在闲鱼上还有卖

啊？关键词是哪个啊 我搜不到啊 都很贵 ![](https://koolshare.cn/uc_server/avatar.php?uid=131594&size=middle) kelvin98373 就想请教下，为什么要刷原版 Openwrt, 是因为你自己定制的插件和主题比较适合吗？ 有什么可以好用的可以分享下吗？ 谢谢 ![](https://koolshare.cn/uc_server/avatar.php?uid=152111&size=middle) starttimes 

> zhangfeideya 发表于 2018-12-29 07:29  
> 啊？关键词是哪个啊 我搜不到啊 都很贵

j1900 四核迷你小主机 ans  试下这个