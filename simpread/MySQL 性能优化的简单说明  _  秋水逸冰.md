\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[teddysun.com\](https://teddysun.com/424.html)

[技术](https://teddysun.com/category/tech) [秋水逸冰](https://teddysun.com/author/teddysun) 发布于: 2015-07-13 更新于: 2015-09-02 18705 次围观 [17 次吐槽](https://teddysun.com/424.html#comments)

[![](https://teddysun.com/wp-content/uploads/2015/mysql.png)](https://teddysun.com/424.html)

MySQL 作为 LAMP 组件中的重要一环，在网站架构中担当关于数据处理的重任。作为目前流行最为广泛的开源数据库，网络上已经有相当多的各种优化教程。本文将试着从改善 MySQL 配置入手，进一步提升 MySQL 的性能。  
关于如何优化数据库结构及 SQL 语句不在本次讨论范围之内。  
MySQL 性能优化我打算分为三个部分，一是物理硬件的优化，二是 MySQL 安装时的编译优化，三是 MySQL 的配置文件 my.cnf 的优化。

**一、物理硬件的优化**  
磁盘 I/O 是制约 MySQL 性能的最大因素之一。  
采用 SSD 的服务器肯定会比普通 HDD 硬盘性能要好；采用 RAID10 的肯定要比单盘的性能要好。  
所谓物理硬件的优化，其实也就是服务器（VPS）硬件的堆砌。更多的内存，更快的磁盘，更强的 CPU 无疑就是最佳的。

**二、MySQL 安装时的编译优化**  
一般情况下不建议直接 yum 安装 MySQL ，一来不能定制功能，二来版本比较老。所以我一般会采取编译安装的方式。  
源码编译安装的前提条件（依赖包）：  
1、CMake。官网：[http://www.cmake.org/](https://www.cmake.org/)   
2、GCC，A working ANSI C++ compiler. GCC 4.2.1 or later。官网：[http://www.gnu.org/software/gcc/](https://www.gnu.org/software/gcc/)  
3、bison，2.1 or newer。官网：[http://www.gnu.org/software/bison/](https://www.gnu.org/software/bison/)  
4、m4。官网：[http://www.gnu.org/software/m4/](https://www.gnu.org/software/m4/)  
5、tar。官网：[http://www.gnu.org/software/tar/](https://www.gnu.org/software/tar/)

编译参数：  
MySQL 5.5.x  
[http://dev.mysql.com/doc/refman/5.5/en/source-configuration-options.html](https://dev.mysql.com/doc/refman/5.5/en/source-configuration-options.html)

MySQL 5.6.x  
[http://dev.mysql.com/doc/refman/5.6/en/source-configuration-options.html](https://dev.mysql.com/doc/refman/5.6/en/source-configuration-options.html)

[LAMP 一键安装脚本](https://teddysun.com/lamp)里对 MySQL 编译的参数如下：  
\-DCMAKE\_INSTALL\_PREFIX=/usr/local/mysql   
\-DMYSQL\_UNIX\_ADDR=/tmp/mysql.sock   
\-DDEFAULT\_CHARSET=utf8   
\-DDEFAULT\_COLLATION=utf8\_general\_ci   
\-DWITH\_EXTRA\_CHARSETS=complex   
\-DWITH\_INNOBASE\_STORAGE\_ENGINE=1   
\-DWITH\_READLINE=1   
\-DENABLED\_LOCAL\_INFILE=1   
\-DWITH\_PARTITION\_STORAGE\_ENGINE=1   
\-DWITH\_FEDERATED\_STORAGE\_ENGINE=1   
\-DWITH\_BLACKHOLE\_STORAGE\_ENGINE=1   
\-DWITH\_MYISAM\_STORAGE\_ENGINE=1   
\-DWITH\_EMBEDDED\_SERVER=1

由于 -DWITH\_DEBUG 默认就是 OFF 状态，所以也无需特别指定此参数。

**三、MySQL 的配置文件 my.cnf 的优化**  
配置文件：  
MySQL 5.5.x  
[https://dev.mysql.com/doc/refman/5.5/en/server-system-variables.html](https://dev.mysql.com/doc/refman/5.5/en/server-system-variables.html)

MySQL 5.6.x  
[https://dev.mysql.com/doc/refman/5.6/en/server-system-variables.html](https://dev.mysql.com/doc/refman/5.6/en/server-system-variables.html)

结合 [LAMP 一键安装脚本](https://teddysun.com/lamp)的 my.cnf 文件，只列出其中 \[mysqld\] 段落中的内容，其他段落内容对 MySQL 运行性能影响甚微，因而姑且忽略。  
介绍一些优化参数。  
\[mysqld\]  
port = 3306  
socket = /tmp/mysql.sock  
skip-external-locking  
#避免 MySQL 的外部锁定，减少出错几率增强稳定性。

key\_buffer\_size = 16M  
#指定用于索引的缓冲区大小，增加它可得到更好的索引处理性能。16M 适用于 512MB 内存，对于内存在 4GB 左右的服务器该参数可设置为 256M，依此类推即可。注意：该参数值设置的过大反而会是服务器整体效率降低！

max\_allowed\_packet = 1M  
#MySQL 根据此配置会限制 server 接受的数据包大小。

table\_open\_cache = 64  
#指定表高速缓存的大小。每当 MySQL 访问一个表时，如果在表缓冲区中还有空间，该表就被打开并放入其中，这样可以更快地访问表内容。注意，不能盲目地把 table\_open\_cache 设置成很大的值。如果设置得太高，可能会造成文件描述符不足，从而造成性能不稳定或者连接失败。  
64 适用于 512MB 内存，1GB 内存则可以设置成 128，依此类推即可。

sort\_buffer\_size = 512K  
#查询排序时所能使用的缓冲区大小。注意：该参数对应的分配内存是每连接独占，如果有 100 个连接，那么实际分配的总共排序缓冲区大小为 100 × 512K ＝ 50MB。  
512K 适用于 512MB 内存，1GB 内存则可以设置成 1M，依此类推即可。

net\_buffer\_length = 8K  
#初始化 server 接受的数据包大小，当需要的时候再由 max\_allowed\_packet 控制增长的大小。注意：该参数值设置的范围只能为 1 – 1024K。

read\_buffer\_size = 256K  
#读查询操作所能使用的缓冲区大小。和 sort\_buffer\_size 一样，该参数对应的分配内存也是每连接独享。  
256K 适用于 512MB 内存，1GB 内存则可以设置成 512K，依此类推即可。

read\_rnd\_buffer\_size = 512K  
#查询操作多表所能使用的缓冲区大小。设置较大的值可以有效提升 ORDER BY 的性能。和 sort\_buffer\_size 一样，该参数对应的分配内存也是每连接独享。  
512K 适用于 512MB 内存，1GB 内存则可以设置成 1M，依此类推即可。

myisam\_sort\_buffer\_size = 8M  
#MyISAM 排序所能使用的缓冲区大小。  
8M 适用于 512MB 内存，1GB 内存则可以设置成 16M，依此类推即可。

max\_connections = 256  
#指定 MySQL 允许的最大连接进程数。如果在访问时经常出现 Too Many Connections 的错误提示，则需要增大该参数值。  
注意：该参数默认值为 151，最大可以设置为 100000  
这里建议设置成内存的一半，比如 512MB 内存就设置成 256，依此类推。

**\[写在最后\]**  
我发现所谓的 MySQL 优化大部分都是来自于官方文档的说明。  
国内的教程要么是很老的，要么是随处转载的，几乎没有多大参考价值。  
没有最优的配置文件，只有适合自己的配置。所以需要结合实际情况，比如内存大小，磁盘 I/O 状况来调整。  
[LAMP 一键脚本](https://teddysun.com/lamp)默认的配置（默认是用于 512MB 内存的 VPS），肯定不是适合你的（是适合我的）。  
而上面只是列举出几个比较重要的参数，更多的参数请参照官方网站。

转载请注明：[秋水逸冰](https://teddysun.com/) » [MySQL 性能优化的简单说明](https://teddysun.com/424.html)