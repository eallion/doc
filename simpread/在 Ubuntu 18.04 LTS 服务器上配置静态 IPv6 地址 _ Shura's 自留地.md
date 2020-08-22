\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[shura.eu.org\](https://shura.eu.org/2018/05/22/%E5%9C%A8Ubuntu-18.04-LTS%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%8A%E9%85%8D%E7%BD%AE%E9%9D%99%E6%80%81IPv6%E5%9C%B0%E5%9D%80/)

今天南洋 pt 开放注册，为了挂 pt，我在 digitalocean 的 vps 上安装了 deluge。可是教育网挂 PT 基本上都是 ipv6，正好 digitalocean 也支持 ipv6，可是没想到踩到 Ubuntu 18.04 的坑上了。

Ubuntu 18.04 的网络接口配置默认使用 NetPlan，这个新工具取代了以前用于配置 Ubuntu 网络接口的静态接口（/etc/network/interfaces）文件。现在必须使用 / etc/netplan/\*.yaml 来配置 Ubuntu 的网络接口。

所以在 digitalocean 配置静态 ip 应该修改 / etc/netplan/50-cloud-init.yaml 文件，填充为一下内容：

```
network:
    version: 2
    ethernets:
        eth0:
            addresses:
            - 公共ipv4地址/20
            - 私有ipv4地址/16
            - 公共ipv6地址/64
            gateway4: 公共ipv4网关
            gateway6: 公共ipv6网关
            match:
                macaddress: MAC地址
            nameservers:
                addresses:
                - 67.207.67.2
                - 67.207.67.3
            set-name: eth0
```

然后输入下面的命令，应用此文件：

```
netplan apply
```

![](https://pic.superbed.cn/item/5cc1c0ff3a213b0417efde12.jpg)

[Configure Static IP Addresses on Ubuntu 18.04 LTS Server – Website for Students](https://websiteforstudents.com/configure-static-ip-addresses-on-ubuntu-18-04-beta/)