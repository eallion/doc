\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[liboy.net\](http://liboy.net/typecho/typecho-to-hexo-and-use-disqus.html)

[从 typecho 迁移到 hexo（评论使用 disqus）](http://liboy.net/typecho/typecho-to-hexo-and-use-disqus.html "从typecho迁移到hexo（评论使用disqus）")
-----------------------------------------------------------------------------------------------------------------------------

1.  [1\. 文章部分](#文章部分)
    1.  [1.1. 使用](#使用)
2.  [2\. 评论部分](#评论部分)
    1.  [2.1. 使用](#使用-1)

从 typecho 迁移到 hexo 还是略微麻烦，除非你不想保持原来 typecho 的永久链接，不然是需要手动去修改。另外一个 disqus 的文章链接也要进行修改。github 搜索了一下，有现成的插件使用。hexo 方面我就不多说了，中文文档说明很清楚。本文主要分成两部分，文章迁移跟评论迁移。

* * *

*   [hexo 中文文档](https://hexo.io/zh-cn/docs/)
*   [typecho2Hexo](https://github.com/NewbMiao/typecho2Hexo)
*   [TypExport](https://github.com/panxianhai/TypExport)

* * *

下载 typecho2Hexo

[](#使用 "使用")使用
--------------

配置:

```
// 根据实际情况更改
$db->connect('localhost','username','password','database');
$prefix = 'tc\_';
```

运行：

```
php converter.php
```

后会自动在当前目录生成你 typecho 的所有文章，放置到 `hexo_path/source/_posts` 下即可。_生成完记得检查文章数目_

* * *

评论我使用的是 disqus，用到的插件是 TypExport，就是从 typecho 导出 WXR 格式，主要用来把评论导入到第三方评论，如果你使用其他第三方评论应该也会支持这种格式。

[](#使用-1 "使用")使用
----------------

点击右侧的`Download ZIP`按钮，下载完成之后解压得到类似`TypExport-master`文件夹，将文件夹重命名为`TypExport`, 上传到 Typecho 目录`usr/plugins`, 然后在后台启用插件。

在后台界面，`控制台`菜单下会有一个`数据导出`菜单，点击进入导出界面，只有一个按钮，我相信你肯定会使用的。

登录 `disqus` 点击 `admin` , 点击 `Community` -> `import`，导入刚刚从 typecho 后台导出的 xml 文件即可。  
关于文章链接的问题，文章数少可以这么做：  
点击 `Community` -> `Discussions` ，点击文章链接，修改即可。  
文章数多建议这么做：  
点击 `Community` -> `Migration Tools` 进行批量修改

* * *

关于 hexo 的配置方面请认真查看文档。

ok! it’s all done~