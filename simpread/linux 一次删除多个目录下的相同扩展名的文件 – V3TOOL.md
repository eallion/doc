\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[v3tool.com\](https://v3tool.com/2019/02/13/linux%E5%88%A0%E9%99%A4%E5%90%8C%E5%90%8D%E6%96%87%E4%BB%B6/)

删除同名文件夹

\# 在当前文件夹及子文件夹下查找. svn 文件夹并递归删除

```
find . -name '.svn' -type d | xargs rm -rf
```

———————-

我想删除某个多层次的文件夹下面的文件，比如是 \*.zip，但这文件存在于很多目录当中，如何用一条命令搞定？

示例：一次性删除某目录及其子目录下所有以. exe 为后缀的文件。

```
find . -name '201702\*.zip'  -type  f  -print  -exec  rm -rf  {} \\;
```

查找前缀名为 201702 后缀 zip 的文件，然后批量删除。

说明：

find：使用 find 命令搜索文件，使用它的 - name 参数指明文件后缀名。

. : 是当前目录，因为 Linux 是树形目录，所以总有一个交集目录，这里根据需要设置

‘201702\*.zip ‘: 指明前缀和后缀名，\* 是通配符

” -type f :” 查找的类型为文件

“-print”: 输出查找的文件目录名

\-exec: -exec 选项后边跟着一个所要执行的命令，表示将 find 出来的文件或目录执行该命令。

注意：exec 选项后面跟随着所要执行的命令或脚本，然后是一对儿 {}，一个空格和一个 \\，最后是一个分号。  
———————  
作者：xufengzhu  
来源：CSDN  
原文：https://blog.csdn.net/xufengzhu/article/details/76981220  
版权声明：本文为博主原创文章，转载请附上博文链接！