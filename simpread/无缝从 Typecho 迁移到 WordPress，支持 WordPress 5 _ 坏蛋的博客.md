\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[www.ibadboy.net\](https://www.ibadboy.net/archives/2617.html)

前言
--

用了一年的 Typecho，总结起来就是各种的不尽人意——长期不更新的系统配合着短缺且不更新的插件…… 凡此种种，令人头疼。

总之，没有一定技术能力的筒子还是不建议用 Typecho，安下心来静静的用 WordPress 就挺好，可以享受社区带来的大量插件和美观的主题，自己只需要更新文章而不必过问技术问题。至于网上关于 WordPress 臃肿不能承载大访问量的言论看看就好，毕竟对于个人博客来讲，谈高负载实在是没有意义 =\_=…

介绍 ByeTyp
---------

当然，如果你不小心已经入了 Typecho 的坑也没关系，因为接下来我就要隆重介绍我的第一个开源项目——**[ByeTyp](https://github.com/sunxiyuan/ByeTyp)** 。

**[ByeTyp](https://github.com/sunxiyuan/ByeTyp)** 是基于 **[TypExport](https://github.com/panxianhai/TypExport)** 二次开发并提供长期维护的一款 Typecho 无缝转 WordPress 的插件。因插件原作者已经超过五年未继续维护项目，且项目本身存在很多 BUG，同时授权方式又是 MIT，所以我就将代码拷贝下来经过修复后发布了全新的 **[ByeTyp](https://github.com/sunxiyuan/ByeTyp)** 项目。

不多啰嗦了，直接介绍下具体迁移流程，当然，好用的话记得给个 Star，如果遇到问题可以在文章下面评论，我会第一时间回复并解决的。

**[ByeTyp](https://github.com/sunxiyuan/ByeTyp)** 迁移的原理是：将 Typecho 中的数据导出为 WordPress 可识别的 WXR 文件。

安装方法
----

访问 **[ByeTyp](https://github.com/sunxiyuan/ByeTyp)** 项目主页：[**https://github.com/ibadboy-net/ByeTyp**](https://github.com/ibadboy-net/ByeTyp) 下载最新版的插件。下载后将插件上传并安装到 Typecho 上。注意上传的时候要为插件的文件夹命名为 ByeTyp，否则插件将无法正常运行。

使用方法
----

启用插件后，按照以下顺序操作，导出当前 Typecho 的数据。

```
控制台->数据导出->导出XML文件
```

当你拿到了后缀为. xml 文件的时候你就离成功近了一大步了。接下来你需要将 xml 文件导入到 WordPress 中。按照这个顺序操作：

```
工具->导入->WordPress->运行导入器（未安装的话就先安装）->选择文件->上传并导入->选择导入的文章所属的用户，之后提示是否导入媒体，随便点就行
```

之后你就会看到你在 Typecho 上的文章、分类目录、标签、评论等数据都出现在了 WordPress 上，但是别急着高兴，因为我们还没能将附件也导入过来。

迁移附件
----

将 Typecho 站点中的 / usr/uploads 目录迁移到 WordPress 的 / wp-content 目录下。之后在数据库中替换图片资源路径，执行以下 SQL 语句：

```
UPDATE wp\_posts SET post\_content = REPLACE( post\_content, '/usr/uploads/', '/wp-content/uploads/');
```

结语
--

至此，迁移工作已经圆满结束，如果遇到任何问题请在本文章下方评论！