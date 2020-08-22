\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[todebug.com\](https://todebug.com/Tips/)

git 和 jupyter 使用小技巧

發佈於 2017-05-25 [評論](https://todebug.com/Tips/#comments) [Tips](https://todebug.com/categories/Tips/ "Tips") 

[](#git "git")git
-----------------

### [](#1-git-push-免密码 "1. git push 免密码")1\. git push 免密码

#### [](#通用情况 "通用情况")通用情况

1\. 使用文件创建用户名和密码

文件创建在用户主目录下：

```
touch .git-credentials
vim .git-credentials
https://{username}:{password}@github.com
```

**记得在真正输入的时候是没有大括号的。**

2\. 添加 git config 内容

`git config --global credential.helper store`

执行此命令后，用户主目录下的. gitconfig 文件会多了一项：`[credential]`

`helper = store`

重新 git push 就不需要用户名密码了。

### [](#使用ssh协议 "使用ssh协议")使用 ssh 协议

首先生成密钥对：

```
ssh-keygen -t rsa -C "youremail"
```

接下来按照提示操作，默认可以一路往下。

然后将生成的位于`~/.ssh/`的`id_rsa.pub`的内容复制到你 github setting 里的 ssh key 中。

复制之后，如果你还没有克隆你的仓库，那你直接使用 ssh 协议用法：`git@github.com:yourusername/yourrepositoryname`克隆就行了。

如果已经使用 https 协议克隆了，那么按照如下方法更改协议：  
`git remote set-url origin git@github.com:yourusername/yourrepositoryname.git`

Done!

* * *

### [](#2-git-add-使用tab键自动补全的中文文件名乱码 "2. git add 使用tab键自动补全的中文文件名乱码")2\. git add 使用 tab 键自动补全的中文文件名乱码

文件名乱码如下所示：

![](https://todebug.com/assets/blog_images/decode_error.png)

**解决方法为：**

`git config --global core.quotepath false`

效果如下：

![](https://todebug.com/assets/blog_images/decode_fixed.png)

可以看出中文已经正确显示了。

* * *

### [](#3-git迁移仓库到另外一个仓库 "3. git迁移仓库到另外一个仓库")3\. git 迁移仓库到另外一个仓库

```
\# 仅保留历史提交信息
git clone --bare yourrepository
```

然后在你的其他服务，比如 gogs 新建一个仓库，然后进入你上步克隆出的仓库中，执行：

```
git push --mirror yourNewRepository
```

然后你就可以删除原来的仓库，然后`git clone`新仓库就行了。

* * *

[](#jupyter "jupyter")jupyter
-----------------------------

### [](#1-jupyter-notebook-创建密码 "1. jupyter notebook 创建密码")1\. jupyter notebook 创建密码

**产生 jupyter notebook 的配置文件：**

```
jupyter notebook --generate-config
```

**生成的配置文件位置为：~/.jupyter/jupyter\_notebook\_config.py**

**打开 jupyter，新建一个 notebook，创建密码以及生成密码的 sha1 密钥，所需代码如下：**

```
from notebook.auth import passwd
passwd()
```

输入一遍你想设置的密码，然后再输入一遍确认，记录下生成的 sha1 密钥值。形式如：‘sha1:xxxxxxx’

然后将这段值按如下格式粘贴到配置文件中对应的`c.NotebookApp.password = u'sha1:xxxx'`位置上，如果你不想寻找文件中的这个位置，你也可以在文件末尾新建一个。

**重启 jupyter，密码生效。**

分享到 [](http://twitter.com/home?status=http://todebug.com/Tips/%20V%20git%E5%92%8Cjupyter%E4%BD%BF%E7%94%A8%E5%B0%8F%E6%8A%80%E5%B7%A7)