# git push 免密码

### 通用情况

1.使用文件创建用户名和密码

文件创建在用户主目录下，打开 Git Bash：

```shell
touch ~/.git-credentials
vim ~/.git-credentials
```
添加一行：
```
https://eallion:TOKEN@github.com
```
`:wq`退出。

2.添加git config内容

```
git config --global credential.helper store
```

执行此命令后，用户主目录下的.gitconfig文件会多了一项：`[credential]`

```
helper = store
```

重新git push就不需要用户名密码了。
