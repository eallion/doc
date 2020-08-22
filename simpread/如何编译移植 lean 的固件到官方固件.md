\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[www.bandwh.com\](https://www.bandwh.com/net/38.html)

BandWh.com • 2019-03-22 12:30 • [](https://www.bandwh.com/net/38.html)[代理 • 路由](https://www.bandwh.com/net/) • 阅读

以我现在的 3865u 软路由为例，移植 lean 的固件，打造最新版本的 Openwrt 固件。

    作为用了 lean 的固件几年的老用户，lean 的固件一直比较稳。lean 的固件是开源的，ssr plus 功能稳定且强大，因此更加有折腾的乐趣。看了好多软路由视频，基本上都是用的 koolshare 的，以前我也用过，觉得不是很稳，主要问题是 koolshare 默认开了多拨均衡，易掉线。另外软件中心有时刷不出来，没法安装科学上网等等。lean 的固件基本没以上问题，编译时候可以根据自己的选择编译出自己的固件。  
   lean 开源的 openwrt 地址是 [https://github.com/coolsnowwolf/lede](https://github.com/coolsnowwolf/lede) ，直接编译肯定能成功。但是 lean 的固件由于某种原因，luci 的版本固化在旧版本，且内核比官方有一定延迟。对于喜欢折腾的我来说，还是希望能用最新的 openwrt 固件来科学上网。

  
[

![](https://www.bandwh.com/uploads/allimg/190322/1-1Z322123610521.jpg)

](https://www.bandwh.com/uploads/allimg/190322/1-1Z322123610521.jpg)

    要编译自己的固件，你是 windows 系统的话，首先可以装上 vmware 虚拟机，再安装 ubuntu18.04 lts 版本，18.10 版本我试了，有一些依赖错误，解决起来稍麻烦，不建议使用。另外编译固件，因为里面有 GFW 不喜的 ss 及 V2ray，不全程翻墙将很难编译成功，将会在编译 ss 及 v2ray 时反复下载程序（因为被屏蔽了），请选择全局翻墙。安装 vmware 及 ubuntu 就略过了，网上教程很多。ubuntu 装好后也装一下 VMware tools，方便拷贝复制文件。安装 VMware tools 的方法是在 ubuntu 里面把 VMware tools 解压到主文件夹，进入到解压后的文件夹。然后运行下列命令进行安装。按提示操作。

```
sudo ./wmware-install.pl 
```

ubuntu 安装处理好了后，在桌面右键 “打开终端”，运行下列命令

```
sudo apt-get update
```

```
sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint
```

依赖包安装好了后，我们克隆 openwrt 及 lean 的包到本地

```
git clone https://github.com/openwrt/openwrt
git clone https://github.com/coolsnowwolf/lede
```

#### \----------------------------------------------------------------------------

注 1：~2019-05-16 lean 删除了 ssr-plus 代码，我们需要对 lean 的 lede 进行下面操作：  
进入 lede 文件夹，右键 “在终端打开” 执行下列命令~

```
git checkout 2915c44a11ca0ee40b51ff5d9c18a0da1951e170
```

~这样 ssr-plus 又回来了。建议把这个文件夹拷贝到其他地方备份，以后 git pull 大雕最新版本时再把备份的 ssr-plus 加到 lede/packgage/lean 里，也不影响后续版本更新。~

注 2：2019-07-08 风平浪静，lean 又恢复了 ssr-plus 安装包，这一步 git checkout 不再需要。

#### \----------------------------------------------------------------------------

这样，我们本地即有 lede 和 openwrt 两个文件夹。lede 文件夹是 lean 的源码，openwrt 文件夹是官方的源码。

下面正式进入移植步骤。以下修改是基于我 esxi 下的软路由进行处理。  
一、拷贝 lede/packgage/lean 文件夹到 openwrt/package 里面  
二、如果你不喜欢新版的 luci 可以修改 openwrt 的 feeds， 在 openwrt/feeds.conf.default 把这个文件换成 lede 下面的同名文件即可，需要最新版的 luci 此步略过。我没做修改，以下我们都是在新版 luci 下面操作。  
三、自定义要安装的包，修改 openwrt 的 include/target.mk 文件，在 DEFAULT\_PACKAGES:=base-files libc libgcc busybox dropbear mtd uci opkg netifd fstools uclient-fetch logd 后面加上自己想要编译的内容，我修改好的文件是这样的

```
DEFAULT\_PACKAGES:=base-files libc libgcc busybox dropbear mtd uci opkg netifd fstools uclient-fetch logd default-settings luci luci-app-aliddns luci-app-upnp luci-app-adbyby-plus luci-app-autoreboot luci-app-ssr-plus ddns-scripts\_aliyun luci-app-vlmcsd luci-app-ramfree luci-app-flowoffload  
```

其中，default-settings luci 必须要有，luci-app-ddns luci-app-upnp luci-app-adbyby-plus luci-app-autoreboot luci-app-ssr-plus ddns-scripts\_aliyun luci-app-vlmcsd luci-app-ramfree luci-app-flowoffload  你根据选择使用。  
把 DEFAULT\_PACKAGES.router:=dnsmasq iptables ip6tables... 其中的 dnsmasq 改为 dnsmasq-full，我修改好的内容见下方。

```
DEFAULT\_PACKAGES.router:=dnsmasq-full iptables ip6tables ppp ppp-mod-pppoe firewall odhcpd-ipv6only odhcp6c kmod-ipt-offload
```

建议把 ip6tables odhcpd-ipv6only odhcp6c 这几个去掉，不然手机浏览有 ipv6 地址的网站时，可能不能访问；另外出国科学上网时也有干扰。  
四、修改目标路由器固件的包，在 / target/linux/x86/Makefile 里 DEFAULT\_PACKAGES 处修改，我就加了个 htop，方便观察，注意不要加 autocore，加了后会和新版 luci 冲突，导致主页错误。**如果你是实体机写盘安装，注意此处要加上相关硬件驱动，可参考 lean 此处的设置。**如果你是只编译一个固件，也可加在上一步的 DEFAULT\_PACKAGES 处。  
五、应用 fullconenat ，拷贝 lede/package/network/config/firewall / 里的 makefile 文件及 patches 文件夹到 openwrt 下面的同目录里，覆盖 openwrt 官方的。  
六、openwrt 官方的活动连接数较少，修改 “活动连接数” 在 package/kernel/linux/files/sysctl-nf-conntrack.conf 里 net.netfilter.nf\_conntrack\_max=16384 修改为 65536，或者更大。  
七、修改主机名和 ssr-plus 彩蛋，openwrt/package/lean/default-settings/files/zzz-default-settings，  在 zzz 文件中 uci set system.@system\[0\].timezone=CST-8 后增加

```
uci set system.@system\[0\].hostname=Openwrt-x86
```

   Openwrt-x86 可以改为你想要的名字  
解封 ssr 彩蛋，在该文件 exit 0 上方适当的位置加上下列命令，安装后可以直接看到 ssr-plus

```
echo 0xDEADBEEF > /etc/config/google\_fu\_mode
```

如果仅是自用固件，可以在该文件 exit 0 上方适当的位置加上加入下列命令，设置 Wan 网口，添加路由器 pppoe 拨号账户密码，装好即可上网

```
uci set network.wan.proto='pppoe'
uci set network.wan.username='宽带账号'
uci set network.wan.password='宽带密码'
uci set network.wan.ifname='eth3'   //我的wan接口是eth3，你要根据自己的路由器情况改
uci set network.wan6.ifname='eth3'
uci commit network   
```

想要修改管理 ip 地址和 lan 口配置，可以在该文件 exit 0 上方适当的位置加上加上下列命令

```
uci set network.lan.ipaddr='192.168.0.8'    //改成你想要默认的管理ip
uci set network.lan.proto='static'          //lan口静态IP方式
uci set network.lan.type='bridge'           //设置桥接
uci set network.lan.ifname='eth0 eth1 eth2 eth4 eth5' //根据自己的路由器情况改Lan口 
uci commit network
```

八、v2ray 及 ssr-puls 版本的处理  
1、如果 v2ray 官方有最新版，我们可以在 openwrt/package/lean/v2ray/makefile 里 PKG\_VERSION:=v4.18.0 修改成最新版本号。（目前 lean 大已经改为预编译好的 v2ray 了，因此此处无需修改）  
2、ssr-plus 修改，在新 luci 下需要处理下，不然安装后不能科学上网，你增加服务器的时候会出现错误。 删除 luci-app-ssr-plus/luasrc/model/cbi/shadowsocksr/server.lua 和 client-config.lua 里的'local ipkg = require("luci.model.ipkg")'  ，新版下就可以输入你 vps 的服务器地址了。

九、以上处理根据习惯处理好了，就可以安装 feeds 包了，打开 openwrt 文件夹，右键 “在终端打开” 运行下列命令

```
./scripts/feeds update -a && ./scripts/feeds install -a 
```

运行好了后我们可以可以对 luci 进行修改。要原汁原味可以不做修改。  
1、openwrt 默认是以 kb 显示内存可用数的，我们可以修改为 MB 显示，在 openwrt /feeds/luci/modules/luci-mod-status/htdocs/luci-static/resources/view/status/index.js 中找到下面的内存处，修改 1024 改为 1048576 ，后面的 kb 改为 MB  
2、在 / feeds/luci/modules/luci-mod-status/luasrc/view/admin\_status/index /10-system.htm 里面把第三个 <div><div width="33%"><%:Architecture%></div><div><%=pcdata(boardinfo.system or "?")%></div></div> 修改为下面的

```
<div><div width="33%"><%:Architecture%></div><div><%=pcdata(boardinfo.system or "?")%>：<%=luci.sys.exec("cat /proc/cpuinfo | grep 'core id' | sort -u | wc -l ")%>Core<%=luci.sys.exec("cat /proc/cpuinfo | grep 'processor' | wc -l")%>Thread</div></div>
```

3、要显示目前 cpu 频率，可以在上面的代码回车后，加上一行

```
<div><div width="33%"><%:CPU Info%></div><div><%=luci.sys.exec("grep 'MHz' /proc/cpuinfo | cut -c11- |sed -n '1p'")%> MHz <%=luci.sys.exec("sensors | grep 'Core 0' | cut -c10-24")%></div></div>
```

十、进行编译，在 openwrt 文佳佳里面右键 “在终端打开” 输入 make menuconfig 命令进行编译  
1、target system 选择 X86，subtarget 选择 x86\_64,target images 里关闭 gzip images。修改固件大小可以在 Kernel partition size (in MB)     Root filesystem partition size (in MB)  进行修改。  
2、luci-application 里面选择你要安装的包，注意把 ssr-plus 下面的都选上，这样可以用 v2ray，ss-libev 进行科学上网，其他根据情况选择。  
退出该界面即可进行编译了。  
十一、进行编译，输入下列命令

```
make -j8 V=s
```

\-j8 还是 j4 根据你 cpu 内核定，我是 9900k，直接 8 核编译，需时大概 15-20min 左右，即可编译好。生成的文件在 openwet/bin/target/x86/64 里面，openwrt-x86-64-combined-squashfs.img 就是我们要的文件，以后升级我们可以在 target images 里打开 gzip images，升级就用 openwrt-x86-64-combined-squashfs.img.gz 文件。

这样我们就获得了我们自定义的 openwrt 官方固件，可以科学上网了。

[

![](https://www.bandwh.com/uploads/allimg/190322/1-1Z32215093M95.jpg)

](https://www.bandwh.com/uploads/allimg/190322/1-1Z32215093M95.jpg)

本地 vmware 下测试的

另外新版 luci 下 lean 的 ssr-plus、flow-offload 文件不能直接重启，需要到固件里 “系统”-"启动项" 里面选择相应模块重启，这样才能重启该模块。为防止 ipv6 干扰 ssr-plus，可以在“网络”-“接口”-“lan” 处“ipv6 分配长度”设为“已禁用”。

本站文章，欢迎转发。转载请注明出处：https://www.bandwh.com/net/38.html