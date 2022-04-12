 ![image-20220310225619746](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220310225619746.png)

![image-20220310225704899](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220310225704899.png)

![image-20220310225827463](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220310225827463.png)

![image-20220310225942194](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220310225942194.png)

![image-20220310230446505](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220310230446505.png)

![image-20220310230512410](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220310230512410.png)

![image-20220310230647251](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220310230647251.png)

银联设计这么复杂是为了保证通信的性能和稳定性。

## MySQL的客户端和服务端连接：

## 1、通信类型（同步/异步）

同步：客户端的调用依赖于被调用方，会受限于被调用方的性能

也就是说，应用去操作数据库，线程会阻塞，一直等待数据库的返回，而且这种同步的过程一般是只能做到1对1，很难做到1对多的通信

异步：1、跟同步相反，能避免应用程序阻塞等待，但是时间并不仅仅是连接的时间，有可能大部分时间是服务端执行SQL语句，因此用异步不能节省在服务端执行SQL语句的时间。2、如果用异步，存在并发的话，肯定不能共用一个连接，每一个SQL语句的执行都需要单独跟服务端建立连接。不然的话就会出现数据干扰、混乱，这样的话每一个通信都建立一个连接，会给服务端带来巨大压力。

综上，我们一般用同步，如果非要用异步，一定要复用连接（如用连接池），不要让每一个操作都去建立一个单独的连接。

## 2、连接方式（长连接/短连接）

MySQL既支持长连接，又支持短连接

短连接特性：只要操作完毕，连接马上关掉。

长连接可以保持打开，不需要频繁地去创建和释放连接，这个连接可以被其它客户端复用。但是长连接会消耗服务端内存，所以对长时间不活动的连接，服务端应该检测到并且把它关掉。

综上，一般来说，我们会在连接池里面用长连接。

![image-20220310232953924](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220310232953924.png)

28800秒为8个小时，即8个小时没活动就会把这个连接关掉。

![image-20220310233316883](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220310233316883.png)

![image-20220310233433885](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220310233433885.png)

![image-20220310233557737](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220310233557737.png)

![image-20220310233719786](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220310233719786.png)

杀死线程连接就断开了

![image-20220310233918493](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220310233918493.png)

![image-20220310234014721](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220310234014721.png)

![image-20220310234145057](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220310234145057.png)

![image-20220310234259952](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220310234259952.png)

最大连接数可以设置为2的14次方，即16384，但连接数不是越大性能就越好

![image-20220310234612827](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220310234612827.png)

不带global默认就是session，而且这种设置值是动态修改，即为服务端重启后会恢复默认，如果想要永久修改，需要改配置文件my.cnf

![image-20220310234804503](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220310234804503.png)

## 3、通信协议（Unix Socket、TCP/IP、Named Pipes、Share Memory)

### Unix套接字：

在Linux和Unix环境下，可以使用Unix套接字进行Mysql服务器的连接；Unix套接字其实不是一个网络协议，只能在客户端和Mysql服务器在同一台电脑上才可以使用。即登录时不用 -h 远程连接。

### 命名管道和内存共享（这两种用的比较少，如果windows下安装时这两个没打勾，是用不到的）

在window系统中客户端和Mysql服务器在同一台电脑上，可以使用命名管道和共享内存的方式，
命名管道开启：–shared-memory=on/off；
共享内存开启：–enable-named-pipe=on/off;

### TCP/IP套接字

任何系统下都可以使用的方式，也是使用的最多的方式，我主要介绍的也是这种方式

其实熟悉操作系统的朋友应该能体会出来，***像前两种，因为客户端和服务端在同一台主机上，也就是一台主机的两个应用，所以这也就是进程间通信的方式，而在不同的主机上就不一样了，就需要网络，tcp/ip建立了***。即用-h远程连接。

## 4、通信方式（单工/半双工/全双工）

![image-20220311091206792](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311091206792.png)

单工：如电视机的遥控器，只能遥控器给电视机发信号

半双工：如对讲机，同一时间只能一个人讲

全双工：打电话，双方可以同时说

**MySQL是半双工**，客户端和服务端同一时间只能有一a个发送数据。

![image-20220311100103075](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311100103075.png)

![image-20220311100241506](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311100241506.png)

4194304是4M，即每次通信最大只能传4M数据，因为是一次性传输，所以大数据量的传输是网络和内存的消耗，因为最好加limit,像navicat一般会默认加limit

## 5、查询缓存（Query Cache)

![image-20220311100840483](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311100840483.png)

![image-20220311100950801](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311100950801.png)缓存默认是关闭的，原因是：1、mysql对执行语句有限制，两次查询的语句必须一模一样，一个空格都不能多2、一张表里的一条数据发生变化，这张表里所有缓存的数据都会失效，如果表更新比较频繁的话，mysql的缓存很鸡肋。所以我们不用，会把mysql的缓存交给专业的服务，如ORM框架，如mybatis默认的一级缓存；或者独立的缓存服务，如Redis

![image-20220311101828778](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311101828778.png)

## 6、语法解析（Parser)

![image-20220311103444085](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311103444085.png)

上面是由语法分析模块处理的

词法解析：把语句打碎成单词

语法解析：如单引号有没有闭合，对单词作分类（是否是关键字、计算符号、变量），最后会得到数据结构：解析树

![image-20220311102943119](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311102943119.png)

中间件如mycat和shardingjdbc，既然要做语句的路由，因此中间件里语法分析和词法分析也是必不可少的

## 7、预处理（Preprocessor)

![image-20220311103423654](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311103423654.png)

![image-20220311104008326](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311104008326.png)

上面是由预处理模块处理的,如表名不存在、列名不存在，然后生成新的解析树

8、查询优化（Query Optimizer)

![image-20220311104315756](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311104315756.png)

将预处理后的解析树生成不同的执行计划，然后从所有的执行计划里选择一种开销最小的方式执行

[https://dev.mysql.com/doc/refman/5.7/en/server-status-variables.html](https://dev.mysql.com/doc/refman/5.7/en/server-status-variables.html)

![image-20220311104648689](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311104648689.png)

![image-20220311105324947](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311105324947.png)

![image-20220311105257505](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311105257505.png)

![image-20220311110740058](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311110740058.png)

![image-20220311111033915](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311111033915.png)

![image-20220311111212105](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311111212105.png)

![image-20220311111354814](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311111354814.png)

![image-20220311111433477](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311111433477.png)

不关闭会消耗资源![image-20220311111504152](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311111504152.png)

![image-20220311112340397](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311112340397.png)

json字符串

![image-20220311112632558](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311112632558.png)

![image-20220311112706300](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311112706300.png)

![image-20220311112951998](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311112951998.png)

在SQL语句前面加explain可查看执行计划的执行方式

8、存储引擎

![image-20220311113237547](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311113237547.png)

表是一种数据结构，存在存储引擎里

![image-20220311113319544](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311113319544.png)

![image-20220311122448499](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311122448499.png)

![image-20220311122549949](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311122549949.png)

![image-20220311122645019](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311122645019.png)

![image-20220311122822675](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311122822675.png)

![image-20220311122915872](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311122915872.png)

![image-20220311124002983](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311124002983.png)

![image-20220311124022366](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311124022366.png)

每个数据库有每个数据库的目录

![image-20220311124145623](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311124145623.png)

![image-20220311124203366](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311124203366.png)

![image-20220311124604827](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311124604827.png)

数据一致性有要求，且要求事务，更新较多用InnoDB

查询多，更新少，可以用MyISAM

非关键数据可以用Memory，存在内存中，快，如果需要临时表可以用这个

CSV文件用逗号分隔，体积小，适合在不同软件间移动，但不支持索引

Archive归档，不支持修改，无索引

NDB作集群

如果上面都不想用，可以自己用C语言写一个

![image-20220311130328991](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311130328991.png)

![image-20220311125801948](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311125801948.png)

由上可见，InnoDB绝大部分都支持

### mysql之frm,MYD,MYI.idb,par文件说明

如数据库a，表b。

1、如果表b采用MyISAM，data\a中会产生3个文件：

b.frm ：描述表结构文件，字段长度等

b.MYD(MYData)：数据信息文件，存储数据信息(如果采用独立表存储模式)

b.MYI(MYIndex)：索引信息文件。

 

2、如果表b采用InnoDB，data\a中会产生1个或者2个文件：

b.frm ：描述表结构文件，字段长度等

如果采用独立表存储模式，data\a中还会产生b.ibd文件（存储数据信息和索引信息）

如果采用共存储模式的，数据信息和索引信息都存储在ibdata1中

如果采用分区存储，data\a中还会有一个b.par文件（用来存储分区信息）

![image-20220311130510351](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311130510351.png)

![image-20220311130526492](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311130526492.png)

# MySQL体系架构

![image-20220311142907919](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311142907919.png)

![image-20220311143004484](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311143004484.png)

![image-20220311143241969](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311143241969.png)

![image-20220311143322007](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311143322007.png)

注：这里的更新指增删改。

![image-20220311143430619](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311143430619.png)

![image-20220311143454077](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311143454077.png)

![image-20220311143512230](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311143512230.png)

DB file在磁盘上，以Page存储，一个Page默认为16K，但是磁盘太慢，所以在内存中划出一片buffer pool，更新时先更新buffer pool，这时内存和磁盘不一致，叫dirtyPage，有很多线程将内存与磁盘一致，叫刷脏

![image-20220311144313703](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311144313703.png)

![image-20220311144653603](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311144653603.png)

![image-20220311145022346](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311145022346.png)

![image-20220311145050826](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311145050826.png)

如果Buffer Pool满了怎么办？跟Redis一样，用LRU，将最近最少使用的剔出去，不一样的是，还会设置young、old

change buffer:如果更新的数据没有唯一索引，并且没有数据重复的情况，不需要去跟磁盘已经存在的数据对比来判断它的唯一性，最终会一次性同步到磁盘，记录到数据页，这叫做merge。什么时候会merge:1、访问数据页到磁盘2、有后台线程定时同步3、正常shutdown4、redo log 写满的时候![image-20220311152209250](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311152209250.png)

写多读少的场景可以调大这个比例

log buffer:为应对崩溃，crash-safe，这样崩了还可以通过日志进行数据恢复

![image-20220311152531176](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311152531176.png)

上面两个文件便是redolog，一个是48M

![image-20220311152632350](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311152632350.png)

先写日志再把数据同步的磁盘的操作叫做WAL，Write Ahead Logging

![image-20220311152933027](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311152933027.png)

为什么要先写日志，再写磁盘？因为日志虽然也在磁盘，但是是顺序I/O，比随机I/O快，提高吞吐量

![image-20220311153327035](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311153327035.png)

![image-20220311153508490](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311153508490.png)

redo log 主要做崩溃恢复，磁盘数据主要还是由内存里的buffer pool刷盘刷出来的。

log buffer什么时候会写入磁盘文件？

![image-20220311154110760](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311154110760.png)

![image-20220311154204771](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311154204771.png)

![image-20220311154542024](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311154542024.png)

![image-20220311154704230](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311154704230.png)

![image-20220311155152386](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311155152386.png)

![image-20220311155213446](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311155213446.png)

![image-20220311155441985](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311155441985.png)

![image-20220311155456575](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311155456575.png)

数据和索引都在独占的表空间里

通用的表空间是自己创建的，

![image-20220311155617865](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311155617865.png)

![image-20220311155629342](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311155629342.png)

![image-20220311155705607](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311155705607.png)

![image-20220311155719141](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311155719141.png)

![image-20220311155844710](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311155844710.png)

![image-20220311160157050](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311160157050.png)

undo，实现回滚，redo，实现崩溃恢复

![image-20220311160349990](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311160349990.png)

![image-20220311160444267](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311160444267.png)

在服务层也有日志文件，binlog，可以被所有存储引擎共用，可以做主从和数据恢复，记录操作DDL和DML

![image-20220311160639541](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311160639541.png)

![image-20220311160817306](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311160817306.png)

![image-20220311161004898](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311161004898.png)

先写内存，再写redolog和undolog，分prepare和commit两个阶段，两个阶段中间有binlog

![image-20220311161412758](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311161412758.png)

![image-20220311165011031](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311165011031.png)

![image-20220311165022792](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311165022792.png)

![image-20220311165143488](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311165143488.png)

![image-20220311165248294](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311165248294.png)

索引可以分两类：主键索引（主索引）和二级索引（辅助索引），创建索引用Creat Index，也可以在创建表之后（add index）

![image-20220311172545981](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311172545981.png)

# 索引到底是什么？

![image-20220311172614868](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311172614868.png)

![image-20220311173827078](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311173827078.png)

![image-20220311173918019](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311173918019.png)

![image-20220311174045098](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311174045098.png)

![image-20220311174210450](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311174210450.png)

![image-20220311174727133](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311174727133.png)

![image-20220311174832996](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311174832996.png)

![image-20220311174856073](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311174856073.png)

![image-20220311174929981](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311174929981.png)

![image-20220311175121277](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311175121277.png)

全文索引用match和against，match跟字段，against跟要查的东西

![image-20220311175330460](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311175330460.png)

![image-20220311180822360](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311180822360.png)

# MySQL索引数据模型推演

![image-20220311180836761](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311180836761.png)

![image-20220311180844791](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311180844791.png)

![image-20220311181031576](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311181031576.png)

 ![image-20220311181117448](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311181117448.png)

![image-20220311181207461](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311181207461.png)

![image-20220311181323416](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311181323416.png)

![image-20220311181335280](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311181335280.png)

![image-20220311181505984](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311181505984.png)

![image-20220311181521504](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311181521504.png)

 ![image-20220311181907405](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311181907405.png)

![image-20220311182456564](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311182456564.png)

![image-20220311182514212](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311182514212.png)

![image-20220311182542669](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311182542669.png)

![image-20220311182703162](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311182703162.png)

![image-20220311182744870](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311182744870.png)

![image-20220311182906586](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311182906586.png)

![image-20220311183024659](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311183024659.png)

![image-20220311183128082](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311183128082.png)

![image-20220311184424003](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311184424003.png)

![image-20220311184832502](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311184832502.png)

![image-20220311184853512](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311184853512.png)

![image-20220311185315330](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311185315330.png)

MySQL使用B+树：关键字数和度一样，只有叶子节点才存数据，叶子节点有序链表（这对排序和范围查找很有效）

![image-20220311185819292](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311185819292.png)

![image-20220311190026533](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311190026533.png)

![image-20220311190122858](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311190122858.png)

![image-20220311190330513](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311190330513.png)

![image-20220311190347373](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311190347373.png)

上面的局限导致红黑树只会放到内存使用，不会放到磁盘使用，如java中的treemap

![image-20220311190715907](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311190715907.png)

![image-20220311190738894](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311190738894.png)

Hash是O(1)，查询快，但是：1、不是按顺序存储，不能排序。只能用=或in等值查询，不能用>或<或between...and。2、数据多了，不可避免产生哈希碰撞，导致性能降低

MySQL的InnoDB中有自适应Hash，但是自己创建的即使创建，也会变成B+树

# 存储引擎中索引如何落地？

![image-20220311191433584](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311191433584.png)

![image-20220311191446145](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311191446145.png)

索引是放到磁盘中的，不是内存

![image-20220311191835542](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311191835542.png)

![image-20220311192025651](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311192025651.png)

![image-20220311214721238](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311214721238.png)

![image-20220311214915201](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311214915201.png)

![image-20220311215032271](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311215032271.png)

聚集（簇）索引：索引的键值的逻辑顺序跟表数据行的物理存储顺序是一致的，如字典的拼音和字。

InnoDB里面，主键索引是聚集索引，因为叶子节点本身就是有序链表。除了主键索引外的索引都叫非聚集索引。

![image-20220311220325646](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311220325646.png)

辅助索引为什么存键值而不是地址：因为页分裂的话地址会变，但指向的键值不会变

没有主键索引（聚集索引）怎么办：1、选用第一个不包含Null的unique key作为聚集索引2、如果1也没有，会选用内置隐藏的6个字节的字段rowid作为聚集索引组织数据存放，且自增

![image-20220311221104978](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311221104978.png)

![image-20220311221529017](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311221529017.png)

# 索引的使用原则

![image-20220311221813828](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311221813828.png)

![image-20220311221858611](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311221858611.png)

![image-20220311222352752](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311222352752.png)

![image-20220311222825263](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311222825263.png)

![image-20220311222917063](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311222917063.png)

![image-20220311231708252](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311231708252.png)![image-20220311231951820](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311231951820.png)

![image-20220311231911149](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311231911149.png)



![image-20220311233115035](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311233115035.png)![image-20220311233500314](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311233500314.png)

![image-20220311233407771](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311233407771.png)

![image-20220311233632545](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311233632545.png)

## ![image-20220311233642881](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220311233642881.png)联合索引最左匹配

![image-20220312114433441](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312114433441.png)

联合索引也叫复合索引，是在多个字段上的索引，

![image-20220312114737649](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312114737649.png)

![image-20220312114938529](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312114938529.png)

![image-20220312115109842](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312115109842.png)

![image-20220312115330499](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312115330499.png)

## ![image-20220312115556932](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312115556932.png)覆盖索引

![image-20220312115906203](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312115906203.png)

### 回表：是在有辅助索引时，除了查询辅助索引外，还要去查主键索引

覆盖索引：要查的列已经在辅助索引里有要查的索引，不用去主键索引再查了

![image-20220312120352080](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312120352080.png)

![image-20220312120940701](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312120940701.png)

![image-20220312121145107](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312121145107.png)

![image-20220312121218294](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312121218294.png)

### 覆盖索引的意义

减少了B+树的扫描，可以减少IO的次数，减少了数据量的访问，大大提升查询性能

所以不要用*，用列名，这样可以使用覆盖索引，避免回表

## 索引条件下推

![image-20220312121828860](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312121828860.png)

![image-20220312121858086](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312121858086.png)

![image-20220312122645548](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312122645548.png)

![image-20220312122714099](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312122714099.png)

出现Using where是说出现了不符合索引的数据，到Service层还要过滤

![image-20220312122844019](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312122844019.png)

![image-20220312122915649](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312122915649.png)

打开后变成了Using_index_condition，也就是说在存储引擎层已经完成了数据的过滤，在服务层就不需要过滤了，如果没有下推，会返回3条姓wang数据，下推后会只返回1条数据,因为存储引擎层过滤了

![image-20220312123116548](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312123116548.png)

![image-20220312123227650](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312123227650.png)

默认是开启的

索引下推的目的是直接在存储引擎层过滤，不需要去服务层过滤，减少了资源的消耗。

![image-20220312124027492](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312124027492.png)

![image-20220312124335212](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312124335212.png)

是数据库自己做的优化，不需要我们操心

![image-20220312142855721](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312142855721.png)

# 索引的创建与使用原则

## 创建索引

![image-20220312142951275](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312142951275.png)

2、索引的个数不要过多：浪费磁盘，创建索引有计算的消耗，数据结构的调整，创建过多有可能影响插入的数据

3、区分度：优化器发现使用索引和全表扫描差不多，会放弃索引

4、会发生数据结构的调整，产生InnoDB页的分裂

5、复合索引：最左匹配，会优先查询前面的

6、创建一个复合的，顶好几个。如Index(a,b,c),包括(a,b,c),(a),(a,b)

7、为节约存储空间，使用前缀作为索引![image-20220312145400279](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312145400279.png)

![image-20220312145110641](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312145110641.png)![image-20220312145521139](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312145521139.png)![image-20220312145547311](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312145547311.png)

13位、14位、15位都是0.84，所以截取13位作为前置索引合适

![image-20220312145133751](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312145133751.png)![image-20220312145829472](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312145829472.png)8、即为什么推荐使用递增的ID作为主键索引？关乎聚集索引，使用UUID等不自增的会导致B+树频繁的分裂与合并。

AVL树（平衡二叉树）、B树（多路平衡查找树）、B+树分别解决了什么问题？

AVL树解决的是二分查找树（BST树）变成斜树，不够平衡的问题。

B树解决AVL树浪费空间，节点存储的关键字不够多导致IO次数过多。

B+树只在叶子节点存储数据，进一步节省空间，IO次数稳定。叶子节点上有顺序访问的指针，提升了范围查找和排序的效率。

## 使用索引

![image-20220312150048630](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312150048630.png)

1、使用函数的结果是不确定的，无法在B+树上用

![image-20220312150223277](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312150223277.png)2、

![image-20220312150400901](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312150400901.png)

![image-20220312150434541](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312150434541.png)

![image-20220312150551213](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312150551213.png)

![image-20220312150625813](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312150625813.png)

3、



![image-20220312151157159](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312151157159.png)

![image-20220312151257078](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312151257078.png)

![image-20220312151309670](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312151309670.png)

最左前缀匹配：注意与联合索引的最左匹配名字不一样，多了前缀

![image-20220312151443391](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312151443391.png)

![image-20220312151636021](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312151636021.png)![image-20220312151706228](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312151706228.png)

由上观之，负向查询并不一定不能用上索引，别太绝对，在某些情况下能用到

![image-20220312151819627](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312151819627.png)

用不用索引，最终由优化器说了算，优化器基于开销，也有基于规则的

![image-20220312152053159](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312152053159.png)

![image-20220312152104705](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312152104705.png)

# MySQL事务与锁详解

![image-20220312152335975](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312152335975.png)

![image-20220312152425493](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312152425493.png)

![image-20220312152439578](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312152439578.png)

什么是数据库的事务？

![image-20220312152453899](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312152453899.png)

![image-20220312152517178](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312152517178.png)

![image-20220312152645467](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312152645467.png)

![image-20220312154300335](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312154300335.png)

只有InnoDB和NDB支持事务

![image-20220312155021214](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312155021214.png)

如果数据页已经被损坏（数据不完整），redolog肯定恢复不了，这时候用double write

其它三个特性都是为了实现一致性

![image-20220312155444549](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312155444549.png)

![image-20220312155452996](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312155452996.png)

![image-20220312155532309](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312155532309.png)

![image-20220312155626550](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312155626550.png)

![image-20220312155640461](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312155640461.png)

![image-20220312155720903](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312155720903.png)

![image-20220312155757648](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312155757648.png)

这时可以用begin或start TRANSACTION,一般用begin

![image-20220312164714909](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312164714909.png)

锁在事务结束的时候释放掉（commit或rollback),或者关掉连接（窗口）也会释放

![image-20220312164917050](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312164917050.png)

![image-20220312165226629](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312165226629.png)

脏读是还没commit

![image-20220312165322058](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312165322058.png)

![image-20220312165448377](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312165448377.png)

![image-20220312165501492](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312165501492.png)

![image-20220312165517665](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312165517665.png)

![image-20220312165747882](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312165747882.png)

![image-20220312165826620](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312165826620.png)

![image-20220312170036318](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312170036318.png)

InnoDB牛逼！在可重复读层面就解决了幻读问题

![image-20220312170138620](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312170138620.png)

![image-20220312170213207](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312170213207.png)

![image-20220312170754597](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312170754597.png)

![image-20220312170853686](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312170853686.png)

![image-20220312171003505](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312171003505.png)

![image-20220312171104377](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312171104377.png)

![image-20220312171324534](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312171324534.png)

![image-20220312171509925](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312171509925.png)

![image-20220312171544500](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312171544500.png)

![image-20220312171733317](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312171733317.png)

![image-20220312171820311](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312171820311.png)

![image-20220312172012469](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312172012469.png)

LBCC和MVCC并不冲突，而是协同合作。

![image-20220312210158975](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312210158975.png)

# MySQL InnoDB 锁的基本类型

![image-20220312210435375](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312210435375.png)

![image-20220312211057710](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312211057710.png)

![image-20220312212041331](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312212041331.png)

![image-20220312211936943](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312211936943.png)

加表锁

页锁是一种特殊存储引擎的锁，这里不讨论

![image-20220312212119066](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312212119066.png)

![image-20220312212209148](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312212209148.png)![image-20220312212318439](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312212318439.png)

![image-20220312212300297](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312212300297.png)

![image-20220312212811284](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312212811284.png)

![image-20220312214502738](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312214502738.png)

![image-20220312215904864](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312215904864.png)

![image-20220312220149038](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312220149038.png)

![image-20220312220233835](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312220233835.png)

![image-20220312220414807](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312220414807.png)

![image-20220312220451923](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312220451923.png)

![image-20220312220541949](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312220541949.png)

![image-20220312220629669](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312220629669.png)

![image-20220312220746897](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312220746897.png)

一个会话就是一个线程，一个并发，一个窗口，一个事务

![image-20220312220848949](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220312220848949.png)

![image-20220313103122455](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313103122455.png)

![image-20220313103318397](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313103318397.png)

意向锁可以大大提高加表锁的效率，因为不用扫描全表

![image-20220313103457224](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313103457224.png)

无论是java还是数据库，加锁都是为了解决资源竞争的问题，控制并发访问

![image-20220313103915416](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313103915416.png)

# 锁的原理：到底锁住了什么？

![image-20220313104224285](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313104224285.png)

![image-20220313104248159](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313104248159.png)

![image-20220313104302324](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313104302324.png)

![image-20220313104320445](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313104320445.png)

![image-20220313104432039](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313104432039.png)

![image-20220313104453712](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313104453712.png)

不加索引，session1只对id=1的锁了，但是明显锁的是表

![image-20220313104648814](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313104648814.png)

![image-20220313104709099](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313104709099.png)

![image-20220313104752681](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313104752681.png)

![image-20220313104835719](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313104835719.png)

![image-20220313104857952](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313104857952.png)

有主键索引时id=1锁了，其它行没锁

![image-20220313105301906](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313105301906.png)

![image-20220313105423743](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313105423743.png)

![image-20220313105459967](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313105459967.png)

![image-20220313105555270](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313105555270.png)

总结：锁的就是索引。

使用primary key 作为聚集索引，没有就用unique key not null作为聚集索引，再没有就用RowID作为聚集索引，所以一张表是不可能没有索引的。

t1没有索引时为什么锁表：没用到索引时，只能对表作全表扫描，把这张表默认的聚集索引全部锁住。

t3主健索引和唯一索引冲突：跟下列有关，先锁辅助索引，再锁主键索引。

以上就是行锁的原理。

![image-20220313110722281](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313110722281.png)

![image-20220313111317960](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313111317960.png)

# 行锁的算法：锁住了什么范围？

![image-20220313112424947](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313112424947.png)

![image-20220313112544538](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313112544538.png)

![image-20220313112817667](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313112817667.png)

字符用ASCII排序

![image-20220313113214601](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313113214601.png)

![image-20220313113321369](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313113321369.png)

间隙锁主要是阻塞插入，但可以再加同样的间隙锁

![image-20220313113557870](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313113557870.png) 

![image-20220313113643940](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313113643940.png)

![image-20220313113821589](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313113821589.png)

![image-20220313134648947](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313134648947.png)

![image-20220313134719485](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313134719485.png)

![image-20220313134806232](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313134806232.png)

![image-20220313134841747](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313134841747.png)

![image-20220313135215475](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313135215475.png)

![image-20220313135313758](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313135313758.png)

![image-20220313135512998](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313135512998.png)

![image-20220313135738332](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313135738332.png)

![image-20220313135828983](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313135828983.png)

![image-20220313135849345](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313135849345.png)

![image-20220313140105832](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313140105832.png)

![image-20220313141652361](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313141652361.png)

![image-20220313141821546](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313141821546.png)解决幻读用MVCC，用的是Gap Lock

## 死锁

![image-20220313141938672](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313141938672.png)

![image-20220313142115915](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313142115915.png)

![image-20220313142249544](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313142249544.png)

![image-20220313142452824](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313142452824.png)

![image-20220313142513423](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313142513423.png)

MySQL自动用图的算法检测到死锁，不用等50S

![image-20220313142832064](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313142832064.png)

![image-20220313143112263](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313143112263.png)

![image-20220313143144361](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313143144361.png)

![image-20220313143219687](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313143219687.png)

![image-20220313143452106](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313143452106.png)

线程干掉，锁自然也被干掉。

![image-20220313143612950](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313143612950.png)

![image-20220313144102890](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313144102890.png)

**![image-20220313144130192](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313144130192.png)**

![image-20220313144221162](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313144221162.png)

![image-20220313144258188](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313144258188.png)

![image-20220313144336406](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313144336406.png)

# MySQL性能优化总结

![image-20220313144522163](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313144522163.png)

## MySQL数据库优化

![image-20220313144549412](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313144549412.png)

![image-20220313145500618](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313145500618.png)

Hikari默认连接池大小是10个

![image-20220313145730532](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313145730532.png)

![image-20220313145908982](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313145908982.png)

![image-20220313150245399](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313150245399.png)

![image-20220313150256855](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313150256855.png)

![image-20220313150355852](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313150355852.png)

![image-20220313150505475](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313150505475.png)

![image-20220313150555439](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313150555439.png)

![image-20220313150647235](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313150647235.png)

![image-20220313150658643](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313150658643.png)

![image-20220313150908893](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313150908893.png)

![image-20220313150925697](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313150925697.png)

![image-20220313151050810](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313151050810.png)

![image-20220313151833115](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313151833115.png)

![image-20220313151924647](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313151924647.png)

![image-20220313152604829](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313152604829.png)

![image-20220313152704446](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313152704446.png)

![image-20220313152725474](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313152725474.png)

![image-20220313152802224](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313152802224.png)

![image-20220313152830813](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313152830813.png)

![image-20220313153058825](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313153058825.png)

![image-20220313153117747](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313153117747.png)

![image-20220313153344764](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313153344764.png)

![image-20220313153409720](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313153409720.png)

![image-20220313153452153](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313153452153.png)

![image-20220313153535406](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313153535406.png)

![image-20220313154001446](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313154001446.png)

![image-20220313154030266](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313154030266.png)

![image-20220313154200060](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313154200060.png)

![image-20220313154418108](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313154418108.png)

![image-20220313154451303](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313154451303.png)

![image-20220313154700075](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313154700075.png)

![image-20220313154929581](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313154929581.png)

![image-20220313155018880](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313155018880.png)

![image-20220313155108528](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313155108528.png)

![image-20220313155210206](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313155210206.png)

![image-20220313155321091](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313155321091.png)

![image-20220313155413880](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313155413880.png)

![image-20220313170254668](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313170254668.png)

![image-20220313170338934](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313170338934.png)

![image-20220313170546513](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313170546513.png)

![image-20220313171023427](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313171023427.png)

![image-20220313171138462](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313171138462.png)

![image-20220313171305717](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313171305717.png)

![image-20220313172642104](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313172642104.png)

![image-20220313172723503](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313172723503.png)

![image-20220313172734669](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313172734669.png)

![image-20220313172749582](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313172749582.png)

![image-20220313172827722](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313172827722.png)

![image-20220313172851558](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313172851558.png)

![image-20220313172944570](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313172944570.png)

![image-20220313173026726](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313173026726.png)

![image-20220313173331123](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313173331123.png)

![image-20220313173446921](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313173446921.png)

![image-20220313173804962](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313173804962.png)

![image-20220313173925290](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313173925290.png)

![image-20220313173944351](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313173944351.png)

![image-20220313174040281](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313174040281.png)

![image-20220313174123457](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313174123457.png)

![image-20220313174248003](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313174248003.png)

![image-20220313174657994](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313174657994.png)![image-20220313180146515](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313180146515.png)

Using index用到了覆盖索引，不需要回表

Using where从存储引擎层返回的还需要在服务层过滤

![image-20220313175040941](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313175040941.png)

![image-20220313175226570](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313175226570.png)

![image-20220313175402799](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313175402799.png)

![image-20220313175432926](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313175432926.png)

![image-20220313175534174](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313175534174.png)

![image-20220313175805109](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313175805109.png)

对视图和触发器、外键：不建议用，因为是不可见的，降低可读性，影响数据库性能，数据库就是来存储数据的，计算的事情不要放到数据库层面来做

图片和文件：存URL

![image-20220313180110227](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313180110227.png)

![image-20220313180211107](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313180211107.png)

数据库架构：主从、分库分表、缓存

![image-20220313180534065](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313180534065.png)

数据库不行，还可以用NoSQL,大数据，搜索引擎

![image-20220313180726032](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220313180726032.png)
