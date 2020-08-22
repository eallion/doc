\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[zhuanlan.zhihu.com\](https://zhuanlan.zhihu.com/p/171564248)

昨晚翻朋友圈，前同事做抖音导流带货的小工作室被平台杀号了，直接把所有账号全部杀停，挺惨~

![](https://picb.zhimg.com/v2-da1d3123521ee4611e943178ea301bd9_b.jpg)![](https://picb.zhimg.com/v2-da1d3123521ee4611e943178ea301bd9_r.jpg)

随手点了个评论又聊了几句，像他们这样的小工作室非常多，内容搬砖，设备集中，再用一点” 技术 “辅助，对平台来说证据早就收集齐了，搞 Anti Spam 行动的时候根据情节喜好选择性的打击一批就完。

想起以前看过抖音的参数，顺手就分享给他，细节很丰富，应该算是我接触的采集最详尽的平台了，仅仅在 App 这种维度的扫描下，没有技术深度的工作室想玩点猫腻几乎不可能，再加上后台的行为分析，有技术深度的工作室也得天天提心吊胆。

抖音走的是普通 https，通过 charles 就可以拦截，看起来并不难，弄明白这些 header 和 body 参数似乎就可以耍耍，但这么大的平台怎么可能这么轻易就被人搞？

![](https://pic3.zhimg.com/v2-f84b2df7e3814f0acbb32a5930cc2f85_b.jpg)![](https://pic3.zhimg.com/v2-f84b2df7e3814f0acbb32a5930cc2f85_r.jpg)

普通的收集 IDFA、IDFV、WIFI 信息都太小儿科了，手上有 2 份抖音的加密参数，是在不同阶段上报的，先看看第 1 份：

![](https://pic4.zhimg.com/v2-fe51d06e57679dc2a7b5e20b181eb3af_b.jpg)![](https://pic4.zhimg.com/v2-fe51d06e57679dc2a7b5e20b181eb3af_r.jpg)![](https://pic1.zhimg.com/v2-658ab797f0e006b93008a27595ed1d58_b.jpg)![](https://pic1.zhimg.com/v2-658ab797f0e006b93008a27595ed1d58_r.jpg)

工作室们手上一般就掌握几十台手机，但是只要不 DFU 模式强刷机，图上红色标记的参数都是不会改变的！哪怕拥有一些改机的技术能力，任凭你怎么改，平台都可以识别你用的是同一台手机。采集的越齐，杀的越准确。

想修改掉第 1 份参数，你就得用代码来完成，那么来第 2 份参数，你会用代码修改，App 就会用代码监控：

![](https://pic1.zhimg.com/v2-954fbc7175a32609e352adb6707f6289_b.jpg)![](https://pic1.zhimg.com/v2-954fbc7175a32609e352adb6707f6289_r.jpg)![](https://pic4.zhimg.com/v2-e6f3cff35d5fcf31416b97802ae440eb_b.jpg)![](https://pic4.zhimg.com/v2-e6f3cff35d5fcf31416b97802ae440eb_r.jpg)![](https://pic3.zhimg.com/v2-e3826f2c04b7c9ade645cc50778b5646_b.jpg)![](https://pic3.zhimg.com/v2-e3826f2c04b7c9ade645cc50778b5646_r.jpg)

好玩吧:)

并且，Charles 只能拦截 https，用一用 wireshark 会发现 App 还往外发 socket。。。

这还是早期抓出来的参数，新版加了多少，是否有其它上报途径，未知。

写下你的评论...  

在欧盟不得罚他两千三亿？

我从来也没说它违法啊

不得不说，第一次玩 https 代理的时候没给手机装证书，翻了一圈手机软件，其他 app 都发现证书错误就请求失败了，只有知乎看到了明文……

太强了

![](https://pic2.zhimg.com/v2-f4bcc55c40efedc78401a3b6c59e50e5_r.gif)