\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[zhuanlan.zhihu.com\](https://zhuanlan.zhihu.com/p/96520671)

1\. 使用 phpinfo 查看 php 版本

![](https://picb.zhimg.com/v2-b4eae66d17790a3815f2e1ea6be00e8c_b.jpg)![](https://picb.zhimg.com/v2-b4eae66d17790a3815f2e1ea6be00e8c_r.jpg)

2\. 下载 igbinary 扩展 [https://windows.php.net/downloads/pecl/releases/igbinary/2.0.8/](https://link.zhihu.com/?target=https%3A//windows.php.net/downloads/pecl/releases/igbinary/2.0.8/)

注意你的 php 版本号 我的是 7.2.1 nts x86

![](https://picb.zhimg.com/v2-3463c598e7afe918ce29601b16e04bf9_b.jpg)![](https://picb.zhimg.com/v2-3463c598e7afe918ce29601b16e04bf9_r.jpg)

3\. 下载 redis 扩展包 [http://pecl.php.net/package/redis](https://link.zhihu.com/?target=http%3A//pecl.php.net/package/redis)

![](https://pic3.zhimg.com/v2-574f126582268a0e2e1930e9cbd9e644_b.jpg)![](https://pic3.zhimg.com/v2-574f126582268a0e2e1930e9cbd9e644_r.jpg)![](https://pic2.zhimg.com/v2-2c4e3080f5736314004ff199d038c3e9_b.jpg)![](https://pic2.zhimg.com/v2-2c4e3080f5736314004ff199d038c3e9_r.jpg)

4\. 解压两个下载文件

![](https://picb.zhimg.com/v2-e8be35611f3c1dfa31357ea4bc94cd87_b.jpg)![](https://picb.zhimg.com/v2-e8be35611f3c1dfa31357ea4bc94cd87_r.jpg)![](https://pic1.zhimg.com/v2-18985c9cf8a3160f281b33bed3b55f37_b.jpg)![](https://pic1.zhimg.com/v2-18985c9cf8a3160f281b33bed3b55f37_r.jpg)

将图上所指文件拷贝到 php/nts/ext 中，重启 phpstudy.

5\. 进入 php.ini 中开启 redis 和 [igbinary](https://link.zhihu.com/?target=https%3A//windows.php.net/downloads/pecl/releases/igbinary/2.0.8/) 扩展包，能搜索到就去掉前面的; 没有添加上即可。

```
extension=php\_igbinary.dll 
extension=php\_redis.dll
```

6\. 刷新 phpinfo 看到如下所示即安装成功。

![](https://picb.zhimg.com/v2-312352f386f045b0a61fa2698cf0436b_b.jpg)![](https://picb.zhimg.com/v2-312352f386f045b0a61fa2698cf0436b_r.jpg)

注意：一定要看好 php 版本号 不然会报错 无法定位程序输入点 xxxxx.

有问题可以私下沟通。

写下你的评论...  

完美，简单明了

![](https://pic2.zhimg.com/v2-90359a720808ff45062287127cfa1039_r.gif)