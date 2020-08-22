\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[segmentfault.com\](https://segmentfault.com/a/1190000017030384)

> 声明：码字不易，转载请注明出处，欢迎文章下方讨论交流。

最近在一个学习小组里学习 AI 的课程，我们所有的学习资料和 homework 都放在 gitlab 上。今天一个小队友从 gitlab 上 load 仓库的时候问起了这个问题，正好在此总结记录一下，仅供参考。

1.git clone
-----------

git clone 顾名思义就是将其他仓库克隆到本地，**`包括被clone仓库的版本变化`**。举个例子，你当前目录比方说是在 e:/course / 中，此时若想下载远程仓库，本地无需**`git init`**, 直接 git clone url（url 是你远程仓库的地址，直接复制就可以了）。执行 git clone 等待 clone 结束，e:/course / 目录下自动会有一个. git 的隐藏文件夹（如果看不见，请尝试设置隐藏文件夹可见），因为是 clone 来的，所以. git 文件夹里存放着与远程仓库一模一样的版本库记录。clone 操作是一个从无到有的**克隆**操作，再次强调不需要`git init`初始化。

### git clone 的用法：

```
$ git clone <版本库的url>
```

例如克隆 TensorFlow：

```
$ git clone https://github.com/tensorflow/tensorflow.git
```

或者使用 SSH 协议：

```
$ git clone git@github.com:tensorflow/tensorflow.git
```

这样就会在本地生成一个目录，该目录与远程仓库同名。  
However，如果本地目录不想与远程仓库同名怎么办？？也有办法，将目录名作为`git clone`命令的第二个参数:

```
$ git clone <版本库的网址> <本地目录名>
```

2.git pull
----------

git pull 是拉取远程分支更新到本地仓库的操作。比如远程仓库里的学习资料有了新内容，需要把新内容下载下来的时候，就可以使用`git pull`命令。事实上，git pull 是相当于从远程仓库获取最新版本，然后再与本地分支 merge（合并）。  
　　即：`git pull = git fetch + git merge`

> 注：git fetch 不会进行合并，执行后需要手动执行 git merge 合并，而 git pull 拉取远程分之后直接与本地分支进行合并。更准确地说，git pull 是使用给定的参数运行 git fetch，并调用 git merge 将检索到的分支头合并到当前分支中。

### git pull 的用法：

```
$ git pull <远程主机名> <远程分支名>:<本地分支名>
```

举例：将远程主机 origin 的 master 分支拉取过来，与本地的 branchtest 分支合并。

```
$ git pull origin master:branchtest
```

如果将冒号和后面的 branchtest 去掉，则表示将远程 origin 仓库的 master 分支拉取下来与本地**当前分支**合并。  
以上的 git pull 操作如果用 git fetch 来表示：

```
$ git fetch origin master:brantest
$ git merge brantest
```

相比起来，`git fetch`更安全也更符合实际要求，因为可以在 merge 前，我们可以查看更新情况，根据实际情况再决定是否合并。

3.git fetch 更新远程代码到本地仓库
-----------------------

理解 fetch 的关键, 是理解 FETCH\_HEAD，FETCH\_HEAD 指的是: 某个 branch 在服务器上的最新状态’。这个列表保存在 .Git/FETCH\_HEAD 文件中, 其中每一行对应于远程服务器的一个分支。  
当前分支指向的 FETCH\_HEAD, 就是这个文件第一行对应的那个分支.  
一般来说, 存在两种情况:

*   如果没有显式的指定远程分支, 则远程分支的 master 将作为默认的 FETCH\_HEAD
*   如果指定了远程分支, 就将这个远程分支作为 FETCH\_HEAD

### git fetch 更新本地仓库的两种用法：

```
\# 方法一
$ git fetch origin master                #从远程的origin仓库的master分支下载代码到本地的origin maste
$ git log -p master.. origin/master      #比较本地的仓库和远程参考的区别
$ git merge origin/master                #把远程下载下来的代码合并到本地仓库，远程的和本地的合并
```

```
\# 方法二
$ git fetch origin master:temp           #从远程的origin仓库的master分支下载到本地并新建一个分支temp
$ git diff temp                          #比较master分支和temp分支的不同
$ git merge temp                         #合并temp分支到master分支
$ git branch -d temp                     #删除temp
```

**码字不易，如对您有帮助，欢迎点赞收藏打赏 ^\_^**