\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[www.jianshu.com\](https://www.jianshu.com/p/10d43bfd17f0)

[![](https://upload.jianshu.io/users/upload_avatars/3986856/296f2f6e-d0c0-45eb-a5d6-05982639d98f.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/6fd1c93143a4)

0.6052018.03.09 20:30:47 字数 44 阅读 9,708

一、删除 php 的相关包及配置

```
sudo apt-get autoremove php7\*
```

二、删除关联

```
sudo find /etc -name "\*php\*" |xargs  rm -rf
```

三、清除 dept 列表

```
sudo apt purge \`dpkg -l | grep php| awk '{print $2}' |tr "\\n" " "\`
```

四、检查是否卸载干净（无返回就是卸载完成）

"小礼物走一走，来简书关注我"

还没有人赞赏，支持一下

[![](https://upload.jianshu.io/users/upload_avatars/3986856/296f2f6e-d0c0-45eb-a5d6-05982639d98f.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/100/h/100/format/webp)](https://www.jianshu.com/u/6fd1c93143a4)

总资产 65 (约 6.10 元) 共写了 1.1W 字获得 47 个赞共 17 个粉丝

### 推荐阅读[更多精彩内容](https://www.jianshu.com/)

*   Spring Cloud 为开发人员提供了快速构建分布式系统中一些常见模式的工具（例如配置管理，服务发现，断路器，智...
    
    [![](https://upload-images.jianshu.io/upload_images/7328262-54f7992145380c10.png?imageMogr2/auto-orient/strip|imageView2/1/w/300/h/240/format/webp)](https://www.jianshu.com/p/46fd0faecac1)
*   百战程序员\_ Java1573 题 QQ 群：561832648489034603 掌握 80% 年薪 20 万掌握 50% 年薪...
    
*   Android 自定义 View 的各种姿势 1 Activity 的显示之 ViewRootImpl 详解 Activity...
    
*   【写在前面】 对部编教材七下《古代诗歌五首》的思考，缘于豫人名师工作室的微课制作任务。反复研读过王君老师的《问君能...
    
    [![](https://upload.jianshu.io/users/upload_avatars/6467661/25fc7552-c891-4710-9c9e-2906b7eefdad.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/48/h/48/format/webp)秋之准备](https://www.jianshu.com/u/9757cf24a6d5)阅读 6
    
    [![](https://upload-images.jianshu.io/upload_images/6467661-f9fb39bc9361f9a1.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/300/h/240/format/webp)](https://www.jianshu.com/p/413d9f15c975)
*   顶着炙热的太阳，漫步于三坊七巷，偶尔驻足下来尝尝著名的福州小吃，流连独特的建筑风格，眼前浮现出一个个耳熟能详的名字...