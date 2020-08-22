\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[www.ifancybot.com\](https://www.ifancybot.com/?p=56)

![](https://www.ifancybot.com/wp-content/uploads/2020/05/%E6%97%A0%E6%A0%87%E9%A2%987.jpg)

前两天看见 win10 2004 的更新，兴高采烈地第一时间进行更新，今天把办公室的电脑也更新了一把，结果发现 WSL2 并没有如传说中的一样，直接包含在 2004 的更新中。

以下是开启 WSL2 的方法（64 位）：

首先右键左下角的 windows 徽标打开最上方的应用和功能

![](https://www.ifancybot.com/wp-content/uploads/2020/05/%E6%97%A0%E6%A0%87%E9%A2%98.jpg) ![](https://www.ifancybot.com/wp-content/uploads/2020/05/%E6%97%A0%E6%A0%87%E9%A2%981-1.jpg)选择右上角的程序和功能 ![](https://www.ifancybot.com/wp-content/uploads/2020/05/%E6%97%A0%E6%A0%87%E9%A2%982.jpg)启用或关闭 Windows 功能 ![](https://www.ifancybot.com/wp-content/uploads/2020/05/WSL3.jpg)适用于 Linux 的 Windows 子系统和虚拟机平台，完成后重启你的电脑。

接着下载并安装 WSL2 升级包：[我是升级包](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

![](https://www.ifancybot.com/wp-content/uploads/2020/05/%E6%97%A0%E6%A0%87%E9%A2%984-3.jpg)到应用商店中搜索 Ubuntu ![](https://www.ifancybot.com/wp-content/uploads/2020/05/%E6%97%A0%E6%A0%87%E9%A2%985-2.jpg)弹出登录 Microsoft 账户的话可以进行登录，但是没有的话直接取消也是可以安装的，多点一次即可。 ![](https://www.ifancybot.com/wp-content/uploads/2020/05/%E6%97%A0%E6%A0%87%E9%A2%986.jpg)直接运行就好了，第一次需要进行安装，大概是几分钟左右；然后设置好自己的账户密码即可食用了。 ![](https://www.ifancybot.com/wp-content/uploads/2020/05/%E6%97%A0%E6%A0%87%E9%A2%987.jpg)安装完成以后:  
1.sudo apt update  
2.sudo apt upgrade  
3.sudo apt install neofetch  
neofetch  
Ctrl+D （大雾 = =）

如果说是已经安装了 linux 发行版而 WSL 还是版本 1 的同学请看：

在安装了上述 WSL 升级包以后打开 powersell 运行：

```
wsl -l -v
```

![](https://www.ifancybot.com/wp-content/uploads/2020/05/%E6%97%A0%E6%A0%87%E9%A2%988.jpg)查看自己的版本也就是 VERSION，如果是 2 就代表 OK 了，是 1 就接着往下

接着运行以下命令进行转换，注意 “Ubuntu-20.04” 应该替换为上方命令运行后显示的 NAME 下面的名称：

```
wsl --set-version Ubuntu-20.04 2
```

![](https://www.ifancybot.com/wp-content/uploads/2020/05/%E6%97%A0%E6%A0%87%E9%A2%989.jpg)这里我是已经转换过了，一般需要个几分钟时间。

最后运行：

```
wsl --set-default-version 2
```

![](https://www.ifancybot.com/wp-content/uploads/2020/05/%E6%97%A0%E6%A0%87%E9%A2%9810.jpg)

文章导航
----