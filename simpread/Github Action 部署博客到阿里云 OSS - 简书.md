\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[www.jianshu.com\](https://www.jianshu.com/p/99952652b2dd)

部署博客有很多选择，国内外都有很多服务可以用，各有各的优缺点：

<table><thead><tr><th></th><th><a href="https://links.jianshu.com/go?to=https%3A%2F%2Fpages.github.com%2F" target="_blank">GithubPages</a></th><th><a href="https://links.jianshu.com/go?to=https%3A%2F%2Fgitee.com%2Fhelp%2Farticles%2F4136" target="_blank">码云 Pages</a></th><th><a href="https://links.jianshu.com/go?to=https%3A%2F%2Fwww.netlify.com%2F" target="_blank">Netlify</a></th><th><a href="https://links.jianshu.com/go?to=https%3A%2F%2Fwww.heroku.com" target="_blank">Heroku</a></th><th><a href="https://links.jianshu.com/go?to=https%3A%2F%2Fwww.aliyun.com%2Fproduct%2Foss" target="_blank">阿里云 OSS</a></th></tr></thead><tbody><tr><td>纯静态托管</td><td>是</td><td>是</td><td>是</td><td>否👍</td><td>是</td></tr><tr><td>CDN 加速</td><td>否</td><td>否</td><td>是👍</td><td>否</td><td>是👍</td></tr><tr><td>访问速度</td><td>慢</td><td>快👍</td><td>一般</td><td>一般</td><td>很快👍</td></tr><tr><td>支持 404 重定向</td><td>否</td><td>是👍</td><td>是👍</td><td>是👍</td><td>是👍</td></tr><tr><td>自定义重定向</td><td>否</td><td>否</td><td>是👍</td><td>是👍</td><td>否</td></tr></tbody></table>

具体选择哪个，根据个人对博客的诉求进行选择。

*   访问速度快：优先选择阿里云 (国内 CDN 加速)、其次是码云 (国内服务器)
*   功能最强：选择 Heroku，支持 Node.js、PHP 等后端

本文章要讲的是如何用 GitHub + Github Action + 阿里云 OSS 部署博客  
因为静态博客系统有很多选择，Jekyll、Hugo、Hexo 等。这里选择 Hexo

Github 地址  
[https://github.com/manyuanrong/oss-blog-example](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fmanyuanrong%2Foss-blog-example)

简书地址  
[https://www.jianshu.com/p/99952652b2dd](https://www.jianshu.com/p/99952652b2dd)

#### 创建项目

```
npm install hexo-cli -g
hexo init blog
cd blog
npm install
hexo server
```

#### 开发和编写博客内容

这一块内容有很多文章讲解，请参考其他文章

#### 提交代码

![](http://upload-images.jianshu.io/upload_images/1771862-2e464454f6b133c8.png)

image.png

代码提交之后并不会发生什么事情。只是保持小步提交的好习惯。接下来我们开始使用 GitHub Action 来做持续集成，生成静态页面。

#### 开通并配置 oss

去阿里云创建一个公共读权限的 Bucket，用来托管我们的静态网站。  
选择香港区域是为了不用备案也能绑定自定义域名。

![](http://upload-images.jianshu.io/upload_images/1771862-edbdf2c6fc9a49a6.png)

image.png

然后我们在阿里云控制台拿到一份 accesskeys。用于后面的远程部署文件到 OSS 上

![](http://upload-images.jianshu.io/upload_images/1771862-565ef73bf1ef58da.png)

image.png

我们将拿到的 accesskeys 配置到 GitHub 项目的 secrets 里面，后面会在工作流脚本中用来掉调用 API 上传文件到 OSS 上面。  
保存在 secrets 里面，这样其他人就不能获取到你的 accesskeys ，保证安全。

![](http://upload-images.jianshu.io/upload_images/1771862-ed9df75fc8e49e1f.png)

image.png

#### 编写 Github Action 持续集成脚本

##### 1\. 创建持续集成配置脚本文件

```
\# 使用mkdir创建目录(windows可以手动建）
mkdir -p .github/workflows
# 使用touch 创建配置文件，名称随意，后缀名为 ".yml" （window可以手动建立文件）
touch ci.yml
```

workflows 下面每个文件就是一个工作流，可以有多个，一般建一个就可以了。

##### 2\. 编写脚本

```
\# workflow的名称，会显示在工作流运行页面
name: MainWorkflow

# 工作流执行的契机：push表示每次push代码之后都会执行
on: \[push\]

jobs:
  # build job 我们用来做持续构建
  build:
    # 构建运行的环境
    runs-on: ubuntu-latest
    # 构建步骤
    steps:
    # 复用 actions/checkout@v1 action，拉取最新代码
    - uses: actions/checkout@v1
```

关于 Action 的详细写法，可以参考官方文档  
[https://help.github.com/cn/github/automating-your-workflow-with-github-actions/about-github-actions](https://links.jianshu.com/go?to=https%3A%2F%2Fhelp.github.com%2Fcn%2Fgithub%2Fautomating-your-workflow-with-github-actions%2Fabout-github-actions)

上面我只写了 actions/checkout 这个 action。这是官方提供的 action，我们直接复用就可以了。它的作用是拉取最新代码

由于我们使用了 Hexo ，因此我们需要使用一个 action 来安装配置 Node.js 环境。  
我们可以去 GitHub 的市场上寻找别人写好的 Action。  
[https://github.com/marketplace?type=actions](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fmarketplace%3Ftype%3Dactions)

我们找到并加入一个叫 `actions/setup-node` 的 action，按照文档我们将工作流脚本进行修改

```
name: MainWorkflow

on: \[push\]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v1
    - uses: actions/setup-node@v1
      with:
        node-version: "12.x"
```

此时我们安装了 Node.js 12，后面的步骤我们就可以开始执行 Hexo 的构建操作了。

我们将配置改成如下

```
name: MainWorkflow

on: \[push\]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v1
    - uses: actions/setup-node@v1
      with:
        node-version: "12.x"
    - name: Build Blog
      run: |
        npm install
        npm install -g hexo-cli
        hexo generate
```

此时我们添加了一个步骤，用于安装 node 依赖，安装 hexo 命令行。最后生成静态页面。

现在我们已经有了生成的静态页面，只需要将它部署到我们的 OSS 上，我们可以使用 `manyuanrong/setup-ossutil` 这个 action 来部署我们的文件

```
name: MainWorkflow

on: \[push\]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v1
    - uses: actions/setup-node@v1
      with:
        node-version: "12.x"
    - name: Build Blog
      run: |
        npm install
        npm install -g hexo-cli
        hexo generate
    - uses: manyuanrong/setup-ossutil@v1.0
      with:
        # endpoint 可以去oss控制台上查看
        endpoint: "oss-cn-hongkong.aliyuncs.com"
        # 使用我们之前配置在secrets里面的accesskeys来配置ossutil
        access-key-id: ${{ secrets.ACCESS\_KEY\_ID }}
        access-key-secret: ${{ secrets.ACCESS\_KEY\_SECRET }}
    - name: Deply To OSS
      run: ossutil cp public oss://enok-blog/ -rf
```

### 提交代码，查看 Action 运行情况

提交我们的代码，这个时候去项目的 Action 菜单下查看运行状态。等一会儿，你将能看到类似下图的情况，表示我们的工作流成功执行，并且将自动生成静态文件并上传到 OSS 上。

![](http://upload-images.jianshu.io/upload_images/1771862-95c6c7218e6f41e7.png)

image.png

我们可以去 OSS 上查看，确实上传成功了！

![](http://upload-images.jianshu.io/upload_images/1771862-649ab1a89a337e48.png)

image.png

每个 OSS Bucket 都会分配一个二级域名。我们可以在地址栏上输入页面的路径进行访问啦

![](http://upload-images.jianshu.io/upload_images/1771862-12b3570059567c5d.png)

image.png

不过此时我们如果省略掉 index.html 的话，并不能正确访问到页面。这是因为我们的 OSS 还没有配置静态网站托管选项。

##### 配置 oss 静态页面托管

在 oss 管理页面 找到 “基础设置” => “静态页面”

![](http://upload-images.jianshu.io/upload_images/1771862-8d2d14ed6c3c1553.png)

image.png

###### 配置默认首页

这样我们可以省略 index.html 访问了

###### 配置默认 404 页面。

这样当我们输入任何不存在的路径是依然能显示首页。这在于一些 SPA 单页应用来说很重要

恭喜，你已经完成了在 OSS 上部署博客的工作！你可以享受 OSS 在国内外飞速的 CDN 服务。还能享受 OSS 提供的各种图片处理服务（压缩图片、缩略图等）

当然，或许你会担心 OSS 收费的问题。但我告诉你，如果只是一个博客，除非真的很多人访问，否则几乎每个月都不会产生什么费用，远远达不到最低收费标准。。。相当于是免费使用的

当然，如果你有自己的域名，不妨在阿里云控制台和 OSS 管理面板上自己探索一下，配置自定义域名访问。以及 HTTPS 等等。