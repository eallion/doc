# 编译 lean openwrt 步骤记录

准备编译环境：

```text
sudo apt-get update
sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler
```

Fork 源码，然后克隆：

```text
cd ~
git clone https://github.com/eallion/lede.git
```

克隆 Aliddns ：

> 如果是用阿里云解析的话，比 `luci-app-ddns` 好用太多。

```text
cd ~/lede/package/lean
git clone https://github.com/chenhw2/luci-app-aliddns.git
pushd package/feeds/luci-app-aliddns/tools/po2lmo
make && sudo make install
popd
```

* 建议用 git subtree 添加 Aliddns：

```text
git subtree add --prefix=package/lean/luci-app-aliddns https://github.com/chenhw2/luci-app-aliddns.git master
```

克隆 Serverchan 微信推送：

```text
cd ~/lede/package/lean
git clone https://github.com/tty228/luci-app-serverchan.git
```

* 建议用 git subtree 添加 Serverchan：

```text
git subtree add --prefix=package/lean/luci-app-serverchan https://github.com/tty228/luci-app-serverchan.git master
```

下载 Openclash：

```text
cd ~/lede
wget https://github.com/vernesong/OpenClash/archive/master.zip
unzip master.zip
cd OpenClash-master
mv luci-app-openclash ../package/lean/luci-app-openclash
```

~~克隆 Shadowsocks-libev~~ ：

> Lean Openwrt 不建议用这个

```text
cd ~/lede/package/lean
mkdir -p package/feeds
git clone https://github.com/shadowsocks/openwrt-shadowsocks.git
```

~~克隆 v2ray-plugin~~ ：

> Lean Openwrt 不建议用这个

```text
cd ~/lede/package/lean
git clone https://github.com/chenhw2/openwrt-v2ray-plugin.git
```

~~克隆 SmartDNS~~：

> Lean Openwrt 不建议用这个

```text
cd ~/lede/package/lean
git clone https://github.com/pymumu/luci-app-smartdns.git
```

Feeds ：

```text
./scripts/feeds update -a
./scripts/feeds install -a
```

配置选项：

```text
make menuconfig
```

LuCI - Collections :

* luci-ssl-openssl

LuCI - Applications :

* luci-app-accesscontrol
* luci-app-aliddns
* luci-app-aria2
* luci-app-arpbind
* luci-app-autoreboot
* luci-app-ddns
* luci-app-filetransfer
* luci-app-firewall
* luci-app-flowoffload
* luci-app-hd-idle
* luci-app-minidlna
* luci-app-nlbwmon
* luci-app-p910nd
* luci-app-ramfree
* luci-app-samba
* luci-app-serverchan
* luci-app-shadowsocks-libev
* luci-app-smartdns
* luci-app-sqm
* luci-app-ssr-plus
* luci-app-ttyd
* luci-app-uhttpd
* luci-app-upnp
* luci-app-usb-printer
* luci-app-verysync
* luci-app-vlmcsd
* luci-app-vsftpd
* luci-app-wol
* luci-app-xlnetacc

Network - Download Manager :

* ariang

Network - File Transfer :

* aria2
* curl
* vsftpd-alt
* wget

Network - IP Addresses and Names

* ddns-scripts
* ddns-scripts\_aliyun
* drill

Network - Web Servers/Proxies :

* pdnsd-alt
* shadowsocks-client
* shadowsocks-libev-config
* shadowsocks-libev-ss-local
* shadowsocks-libev-ss-redir
* shadowsocks-libev-ss-rules
* shadowsocks-libev-ss-erver
* shadowsocks-libev-ss-tunnel

Network :

* acme
* acme-dnsapi
* shadowsocks-libev
* trojan
* v2ray-plugin
* 去掉 wpad

Extra packages ：

* ipv6helper

预下载：

```text
make download V=s
```

开始编译：

```text
make -j8 V=s
```

如果是真机编译环境，-j 后面的参数可以设为实际CPU核心数的2倍。虚拟机还是老老实实用 -j1 。

摘取新源码：

```text
git pull
```

编译新固件：

```text
./scripts/feeds update -a
./scripts/feeds install -a
```

```text
make clean
make menuconfig
make download V=s
make -j8 V=s
```

其他 make 参数：

```text
make --help #查看 make 选项
make download # 仅下载make需要的文件
make defconfig # 默认配置
make package/xxxxxxxxx/compile # 构筑单个包
make clean  # 清除`/bin`和`/build_dir`文件夹
make dirclean  # 清除编译完成的文件和相对应工具链，相对应全面清除
make distclean  # 相对上面会清除配置和feeds
```

L大的项目地址：

[coolsnowwolf/lede](https://github.com/coolsnowwolf/lede)

添加一些其他的APP：

[shadowsocks/openwrt-shadowsocks](https://github.com/shadowsocks/openwrt-shadowsocks)

[honwen/openwrt-v2ray-plugin](https://github.com/honwen/openwrt-v2ray-plugin)

[honwen/luci-app-aliddns](https://github.com/honwen/luci-app-aliddns)

[pymumu/luci-app-smartdns](https://github.com/pymumu/luci-app-smartdns)

[tty228/luci-app-serverchan](https://github.com/tty228/luci-app-serverchan)

