\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[www.138vps.com\](https://www.138vps.com/vpsjc/472.html)

发布时间：2016-5-14 10:10 Saturday 作者：[苏苏](https://www.138vps.com/author/1 " admin@138vps.com") 阅读（8990）

我们购买 vps 的时候，比较关心的是产品的费用，速度以及商家的服务稳定性。但是很多时候我们都很困惑，为什么差不多的产品，价格却相差这么大，这就需要我们对产品进行对比，看懂不同产品的配置信息了。免得高价购买了配置差的产品。

这次我们先看看 CPU，苏苏就以 LVMLA 的 12 刀年付 vps 为例，简单讲讲如何查看 CPU。

1、查看 cpu 的常见命令

cat /proc/cpuinfo

[![](http://www.138vps.com/content/uploadfile/201605/f3cc1463192891.jpg)](http://www.138vps.com/content/uploadfile/201605/f3cc1463192891.jpg)

其中几个主要的参数含义：

processor：逻辑处理器的 ID

model name：CPU 型号

cpu cores：相同物理封装处理器中的内核数

siblings：相同物理封装处理器中逻辑处理器数

2、查看物理 CPU 个数

cat /proc/cpuinfo| grep "physical id"| sort| uniq| wc -l

[![](http://www.138vps.com/content/uploadfile/201605/15601463192923.jpg)](http://www.138vps.com/content/uploadfile/201605/15601463192923.jpg)

3、查看逻辑 CPU 个数

cat /proc/cpuinfo |grep "processor"|wc -l

4、查看每个 CPU 中的核心数

cat /proc/cpuinfo| grep "cpu cores"| uniq

5、查看 CPU 主频

cat /proc/cpuinfo |grep MHz|uniq

[![](http://www.138vps.com/content/uploadfile/201605/799b1463192934.jpg)](http://www.138vps.com/content/uploadfile/201605/799b1463192934.jpg)

6、每个物理 CPU 中的逻辑 CPU

cat /proc/cpuinfo | grep "siblings"

这里我们需要得到一个公式计算：

A - 总核数 = 物理 CPU 个数 X 每颗物理 CPU 的核数

B - 总逻辑 CPU 数 = 物理 CPU 个数 X 每颗物理 CPU 的核数 X 超线程数

这里，苏苏再分享几个我们在 VPS 中常用的几个命令。

1、查看 VPS 系统的位数，比如 32 位还是 64 位

uname -a

2、查看系统运行时间、用户数

uptime

3、查看当前目录大小

du -sh

这个可以帮助我们查看是否有大的文件。

4、查看操作系统版本

head -n 1 /etc/issue

5、查看磁盘分区

fdisk -l

查看分区情况，看看是否有需要挂载数据盘。

6、查看内存使用情况

free -h

7、查看进程情况

topp

**特别申明：**若无说明, 文章均为原创，转载时请注明本文地址，谢谢合作！  
**本文链接：**[http://www.138vps.com/vpsjc/472.html](http://www.138vps.com/vpsjc/472.html "如何查看linux vps 的CPU配置，及看懂参数")

本站仅为分享信息，绝对不是推荐，所有内容均仅代表个人观点，读者购买风险自担。如果你非要把风险推苏苏头上，不要这么残忍，好吗？

本站保证在法律范围内您的个人信息不经由本站透露给任何第三方。

所有网络产品均无法保证在中国任何地区, 任何时间, 任何宽带均有相同的访问体验, 那种号称某机房绝不抽风的不是骗子就是呵呵.

任何 IDC 都有倒闭和跑路的可能, 备份永远是最佳选择, 服务器也是机器, 不勤备份是对自己极不负责的表现.

[加入群 1：569839985](https://shang.qq.com/wpa/qunwpa?idkey=a9d579dbd1974923fe5919191d56dd25ab8f8d8830800a408c5390710dc01685)

欢迎 IDC 提交优惠信息或者测试样机，提交信息请 Eamil 至 admin@138vps.com，苏苏不保证一定会进行发布。

但请 IDC 留意以下内容：

无官方正式首页、无可用联络方式暂不发布；

曾经有过倒闭和跑路经历者重开不到 6 个月不做发布；

从本日起（2016-07-18）不接受任何形式的免费赞助和 VPS 馈赠，不接受任何评测报告的投稿，不接受任何付费发布和付费删除评论，所有 IDC 若有必要提交测试样机，请在 7 日后自行删除。