\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[sspai.com\](https://sspai.com/post/61052)

### Matrix 精选

[Matrix](https://sspai.com/matrix) 是少数派的写作社区，我们主张分享真实的产品体验，有实用价值的经验与思考。我们会不定期挑选 Matrix 最优质的文章，展示来自用户的最真实的体验和观点。

文章代表作者个人观点，少数派仅对标题和排版略作修改。

前排提醒，要实现本文所述的效果，需要使用到的工具是：

*   [女娲石](https://play.google.com/store/apps/details?id=com.oasisfeng.nevo&hl=zh) - 使微信能够快捷回复
*   [Tasker](https://play.google.com/store/apps/details?id=net.dinglisch.android.taskerm&hl=zh)  
    
*   [Notification Listener](https://play.google.com/store/apps/details?id=com.balda.notificationlistener&hl=zh) - Tasker 的插件，提供了通知的触发和操作接口
*   图灵机器人 - 一个提供 Web Api 的对话机器人

另外额外需要一些条件：

*   对 Android 手机、Tasker 有一定的了解。能按照 [这个教程](https://sspai.com/post/45759) 完全自己操作一遍，完成本篇文章的操作应该就没有问题
*   能通过 Google Play 购买并下载应用

实际我的手机环境是一个一加 8 Pro，系统是 Oxygen OS，已 Root。如果是其他系统的话，需要自己搞定所涉及的应用不被系统杀掉（一般是电池管理不优化并给应用加锁）以及管理通知权限。

前言
--

以前玩机的时候接触并在 Google Play 上购买了 tasker，但是每次都是难以上手、耗电、不知道需要自动化什么任务放弃使用了。这次突然想给自己的微信增加一个自动回复的功能， 像以前 QQ 的离线回复一样，稍微研究了一下怎么利用已有的工具实现，理论上来说也不算任何「外挂」程序， ~应该不会被微信官方封号~ 。

整个自动回复的流程大概是这样的：

1\. 微信通知事件被 Tasker 捕获

2\. Tasker 解析出通知的文本并通过图灵机器人 Api 上传

3\. 图灵机器人回传的文本通过 Tasker 回复此通知事件

![](https://cdn.sspai.com/2020/06/20/62ed16f0c39d5faccce599dd8de48b7c.png) 大致流程

热身
--

在实现前面所述的效果之前，我们先来通过一个简单的自动回复的例子来熟悉一下 Tasker 操作的流程。这里不需要用到图灵机器人，也不用接触 JavaScript 。

### 触发事件

首先设置 Tasker 的事件，这里直接采用 Tasker 自带的通知事件进行触发。点击右下角的加号，选择事件 - 界面 - 通知，按照截图中的方式输入：

*   **所有者程序** ：微信和 Pushbullet，后者完全是为了测试用，因为我可以在电脑浏览器给自己手机发消息从而触发事件，验证流程；
*   **文字** ：这里匹配两个文本，「在吗」或「跟我说话」，中间的斜杠表示「或」的概念，当然你要在后面再过滤也是可以的，在这里添加可以避免所有的通知都要走后面的操作。

### 任务编辑

之后进入任务编辑的界面，这里就是实现两个 `if` 逻辑，分别匹配之前输入的文本。

![](https://cdn.sspai.com/2020/06/20/de9cf9b164c8aa48818aea2a0b4647bc.png)

这里需要注意两个地方：

*   `if` 操作中 `%evtprm` 是 `Event Context` 中的内容，即事件的上下文参数，是一个数组。`%evtprm3` 是数组的第三个元素，对于通知事件来说就是通知的文本内容（`%evtprm2` 是标题）。Notification Listener 同样提供了 `%nltext` 作为通知的文本变量，使用这个也是一样的。`~R` 表示正则匹配，即匹配到「在吗」就会走第一个逻辑。
*   具体执行的回复操作是通过 Notification Listener 实现的，`%nlkey` 是它提供的变量，直接填上并加上回复信息就行。

### 通过女娲石使微信支持快捷回复

这里还有一个问题，微信本身是不支持快捷回复的，这里就需要女娲石来实现这样一个按钮，我的手机已 Root，因此能够微信的身份发送通知，之前的所有者程序选择微信，是没有问题的。没有测试过普通模式下的效果，理论上也是可以的，只需要把之前的所有者程序加上女娲石即可。

![](https://cdn.sspai.com/2020/06/20/a559ede5c3814ec49040bf94b061b40a.png)

激活配置之后，现在收到微信消息，就会自动回复消息了。

进阶
--

显然我们不仅仅满足于此，以上是基本实现了 QQ 离线消息的效果，让人一下子穿越回十几年前盯着别人 QQ 上下线的年代。现在我希望自己完全变成一个没有感情的机器人，不再受世间的纷纷扰扰。

有了热身的基本原理，我想大家应该已经明白了，获取通知文本、回复微信消息的方法。现在只需要一个机器人的接口，我们把文本输进去，它把回复吐出来，然后接上之前的流程就可以了。

### 找一个机器人

一番搜索之后确定了图灵机器人，因为它提供了 [Web API](https://www.kancloud.cn/turing/www-tuling123-com/718227)。个人用户一天的调用上限是 100 次，和朋友玩玩是完全够了。

![](https://cdn.sspai.com/2020/06/20/1eb499aba2fce4116dc403393dba6497.png) 图灵机器人

### 触发事件

触发事件可以依然按照之前使用的 Tasker 自带的通知事件，这里我使用的是 Notification Listener 提供的 `Posted Apps`。

### 略带挑战的任务编辑

建立一个如图的操作，对，Tasker 是支持 JavaScript 的，这样就可以很方便的进行 Web Api 的调用。这里遇到了这个任务里面最大的困难。首先对于 JavaScript 不是特别熟悉，其次 Tasker 的 js 还有点不太一样的地方。

对于 Tasker 的 JavaScriptlet 来说，如果勾选了「自动退出」，则会在执行到最后一行之后退出程序，那么对于异步的网络请求和更改变量就会不起效果；否则的话，需要自行调用 `exit()` 来告诉 Tasker 何时退出。这里有一个坑是在异步的请求里，直接对 tasker 的 Local 变量赋值是不起作用的，需要调用 `setLocal` 来赋值。

```
var xhr = new XMLHttpRequest();
var url = "http://openapi.tuling123.com/openapi/api/v2";
var response = "default";
xhr.open("POST", url, true);
xhr.setRequestHeader("Content-Type", "application/json");
xhr.onreadystatechange = function () {
  if (xhr.readyState === 4 && xhr.status === 200) {
    var json = JSON.parse(xhr.responseText);
    response = json.results\[0\].values.text;
    flash(response);
    setLocal("response", response);
    exit();
  }
};
var text = nltext;
var str = {
  reqType: 0,
  perception: {
    inputText: {
      text: text,
    },
    selfInfo: {
      location: {
        city: " 杭州 ",
        province: " 浙江 ",
      },
    },
  },
  userInfo: {
    apiKey: "<Your ApiKey>",
    userId: "<Your UserId>",
  },
};
var data = JSON.stringify(str);
xhr.send(data);
```

![](https://cdn.sspai.com/2020/06/20/9dedb22a372e4542dca9d1ecfb8cf91e.png)

当然可以完全忽略上一段，直接把这段代码中的 `apiKey` 和 `userId` 更改为你的机器人的 API 密钥以及用户名。如果你有兴趣，我们可以简单描述一下这段代码的细节：

*   `var test = nltext`，这里是把 Notification Listener 的 `%nltext` 变量赋值并后面拼接在 JSON 请求里面。虽然显得有点多余，但是你可以把 `nltext` 变成确定的字符串，来测试你的代码是否能正确从服务器拿回请求（按下编辑页面里面的播放键）。
*   `flash()` 会生成一个 Toast 提示，也就是每次回复的消息会在下方提示内容。
*   JSON 请求里面的 `location` 是机器人的默认地址，也就是说如果问它天气怎么样，会告诉我杭州的天气。

### 测试效果🎉

现在就可以找个小伙伴测试一下你的机器人啦，在工作时段打开静音模式，让机器人来回复那些消息吧。

![](https://cdn.sspai.com/2020/06/20/187f40dff722d4740f71ceeb30aa73ea.png)

注意事项
----

当然 **最后一个提醒** ，如果有群聊通知没有开免打扰、或者在群里被 @，还是会回复的，以免再工作群里回复一些莫名其妙的话，可以考虑像热身这一节所讲的，做在通知标题 `%nltitle` 上做一些过滤，制定一个白名单。

\> 下载少数派 [客户端](https://sspai.com/page/client) 、关注 [少数派公众号](https://sspai.com/s/J71e) ，了解更精彩的数字生活 🍃