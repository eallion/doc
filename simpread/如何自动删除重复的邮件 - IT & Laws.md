\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[itlaws.cn\](https://itlaws.cn/post/how-to-remove-duplicate-emails/)

因为依赖 Gmail 的邮件搜索功能，所以我一直使用 Gmail 管理我的邮件：在 Gmail 中，使用 pop 协议收取其他邮箱的信件，并在 Gmail 中调用 smtp 协议去回复邮件。

是的，你收到的、看起来是我 QQ 邮箱、126 邮箱、办公邮箱等各种邮箱发过去的邮件，实际上都是我在 Gmail 上发送过去的。

有一段时间，我曾经将我的域名 `zhoucaiqi.com` 托管到 Google 的企业邮局并给自己开设了邮箱 [\`email@zhoucaiqi.com](mailto:%60email@zhoucaiqi.com)`，并将我积累了多年的` [zhoucaiqi@gmail.com](mailto:zhoucaiqi@gmail.com) `的邮件导入到`[email@zhoucaiqi.com](mailto:email@zhoucaiqi.com)`。但是，Google企业邮局有各种各样的问题，导致我被迫回归` [zhoucaiqi@gmail.com](mailto:zhoucaiqi@gmail.com)\` 。因为网络问题、服务器限制问题、担心导入不全的问题，我多导入了一两次，导来导去之后，就出现了很多重复的邮件。

我购买的 200G 空间，已经快被 Gmail 用满，所以需要删除重复的邮件了。

因为重复的邮件有数千或数万封，靠人工去筛选、删除，是不现实的。而 Gmail 官方又没有提供自动筛选、删除的功能。因此，只能自己想办法。

`imap`是邮件同步协议，能让本地客户端的邮件内容与邮件服务器端的内容同步。因此，可以考虑使用`imap`协议将邮件下载到本地，然后在本地进行重复邮件的筛查、过滤、删除。

说干就干。

先在 Gmail 的设置中启用`imap`协议，然后安装邮件客户端 [thunderbird](https://www.thunderbird.net/zh-CN/)，然后把 Gmail 账号信息设置到`thunderbird`。`thunderbird`默认就采用`imap`协议。`thunderbird`默认只同步邮件头信息，但即使如此，我十几万封的邮件，依然同步了一个晚上，可能是受限于 Gmail。

接着，给`thunderbird`安装`Remove Duplicates`扩展（[Link](https://addons.thunderbird.net/en-US/thunderbird/addon/remove-duplicates/)），这扩展是一款自动筛查重复邮件的插件，可通过很多参数去判断两封邮件是否属于重复邮件，例如 `message ID`、`date in seconds`、`subject`、`from`等。在邮件的文件夹中，鼠标右键可以选择通过哪些参数判断邮件是否属于重复的邮件。

我觉得默认的参数就 OK 了。

我先在某个子文件夹做了测试，这子文件夹有 5 万封邮件，在文件夹鼠标右键选择`Remove Duplicate Messages`之后，两三分钟就筛选完了，筛选出来 5 千封重复的邮件。看筛选结果，是正确的。

我的 Gmail 总共有 14.1 万封邮件，我根文件夹选择`Remove Duplicate Messages`之后，大概十分钟后，过滤出 7 万封重复的邮件：

![](https://itlaws.cn/img/202001/thunderbird-remove-duplicates.png)

重复的邮件中，其中一封邮件标记为`Keep`，其他邮件标记为`Del`。点击右下角的`Delete Selected`就可以删除重复的邮件了。

`imap`的同步特性，会把这个删除操作同步到服务器端。

done。

文章作者 zhoucaiqi@gmail.com

上次更新 2020-01-30 [(993aac3)](https://github.com/xianmin/hugo-theme-jane/commit/993aac3f1ac7dbcac0d12f54df02198040a2b00d "update how to remove duplicate emails")  
update how to remove duplicate emails

许可协议 [CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/)

赞赏支持

 ![](https://itlaws.cn/img/wechat-reward.jpg) 微信打赏 ![](https://itlaws.cn/img/alipay-reward.jpg) 支付宝打赏