![image-20220330154940097](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330154940097.png)

![image-20220330155053526](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330155053526.png)

![image-20220330155157512](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330155157512.png)

![image-20220330155243336](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330155243336.png)

![image-20220330155312746](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330155312746.png)

![image-20220330161020613](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330161020613.png)

![image-20220330165459592](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330165459592.png)

![image-20220330165541615](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330165541615.png)

![image-20220330165723450](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330165723450.png)

![image-20220330165827027](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330165827027.png)

# 第2章 并发基础

## 2-1 CPU多级缓存-缓存一致性

![image-20220330171118832](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330171118832.png)

## ![](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\4.jpg)![image-20220330171225655](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330171225655.png)![image-20220330183721295](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330183721295.png)![image-20220330184242004](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330184242004.png)2-2 CPU多级缓存-乱序执行优化

![image-20220330185028093](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330185028093.png)

注：乱序优化单核没问题，多核可能有问题，因为每个核都有自己的缓存

## 2-3 JAVA内存模型

![image-20220330185405862](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330185405862.png)

![image-20220330185906032](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330185906032.png)

![7](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\7.jpg)

![image-20220330190406089](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330190406089.png)![image-20220330190511672](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330190511672.png)![image-20220330190617425](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330190617425.png)![image-20220330190713744](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330190713744.png)![image-20220330190753196](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330190753196.png)![image-20220330190825252](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330190825252.png)

![image-20220330190918713](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330190918713.png)

![image-20220330191544442](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330191544442.png)

## 2-4 并发的优势与风险

![10](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\10.jpg)![image-20220330192412720](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330192412720.png)

# 第3章 项目准备

![image-20220330194255706](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330194255706.png)![image-20220330195931749](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330195931749.png)![image-20220330200154090](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330200154090.png)

countdownlatch和semaphore通常和线程池一起使用

# 第4章 线程安全性(原子性、可见性、有序性)

![image-20220330200933143](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330200933143.png)![image-20220330203137734](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330203137734.png)![image-20220330233435256](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330233435256.png)![image-20220330233220747](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330233220747.png)![image-20220330233406925](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330233406925.png)![image-20220330234734329](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330234734329.png)![image-20220330235106451](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330235106451.png)![image-20220330235200045](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330235200045.png)![image-20220330235258666](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330235258666.png)![image-20220330235356137](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330235356137.png)![image-20220330235523355](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330235523355.png)![image-20220330235651073](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330235651073.png)![image-20220330235737210](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220330235737210.png)volatile读写都是在CPU指令级别操作的，没有原子性，有可见性和有序性

使用场景：两个条件：1、对变量的写操作不依赖于当前值  2、该变量没有包含在具有其它变量的不变的式子中 **综上，volatile特别适合作为状态标记量使用，此外，还适合double check**

![image-20220331000210563](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220331000210563.png)![image-20220331001018325](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220331001018325.png)![image-20220331001156248](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220331001156248.png)![image-20220331001251775](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220331001251775.png)![image-20220331001423841](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220331001423841.png)

如果两个操作的执行顺序无法从Happens-Before原则推导出来，就不能保证有序性，JVM就可以对其重排序![image-20220331001848557](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220331001848557.png)

# 第5章 安全发布对象

![image-20220331105333157](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220331105333157.png)![image-20220331105626651](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220331105626651.png)![image-20220331105820477](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220331105820477.png)

![image-20220331110039301](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220331110039301.png)从上可以看出，直接修改了私有数组，因此不安全![image-20220401120103036](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401120103036.png)

# ![image-20220401110655087](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401110655087.png)![image-20220401114703813](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401114703813.png)![image-20220401115409516](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401115409516.png)第6章 线程安全策略

![image-20220401153708638](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401153708638.png)![image-20220401153826483](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401153826483.png)![image-20220401154503463](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401154503463.png)![image-20220401155105940](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401155105940.png)![image-20220401160404090](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401160404090.png)![image-20220401160249559](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401160249559.png)![image-20220401170301545](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401170301545.png)![image-20220401170507420](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401170507420.png)![image-20220401192820135](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401192820135.png)![image-20220401192420160](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401192420160.png)![image-20220401192923541](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401192923541.png)![image-20220401193138007](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401193138007.png)![image-20220401193821171](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401193821171.png)![image-20220401195813159](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401195813159.png)![image-20220401194823133](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401194823133.png)这两个在循环时不要做更新操作，否则报异常，推荐用for循环

多线程下：用synchronized或lock做同步措施，同时可以使用并发容器，如CopyOnWriteList

## 注意：工作中使用并发容器比同步容器多

![image-20220401202021177](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401202021177.png)![image-20220401202346778](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401202346778.png)![image-20220401202556569](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401202556569.png)CopyOnWriteList缺点:都是复制副本，占内存导致频繁GC，同时不能用于实时读（适合读多写少，虽然能做到最终一致性),慎用，互联网中不知多少数据时可能会引起故障。

CopyOnWriteList设计思想：1、读写分离（读时不加锁在原数组上读，写时加锁复制副本）2、最终一致性3、使用时另外开辟空间，用这种方式解决并发冲突 ![image-20220401201132663](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401201132663.png)![image-20220401201213753](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401201213753.png)![image-20220401203023095](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401203023095.png)![image-20220401203223977](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401203223977.png)![image-20220401203313489](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220401203313489.png)

# 第7章 J.U.C之AQS（AQS是JUC的核心) 

![11](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\11.jpg)![image-20220407162431364](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407162431364.png)![image-20220407162506408](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407162506408.png)![image-20220407163204287](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407163204287.png)![image-20220407163229612](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407163229612.png)![image-20220407163257162](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407163257162.png)![image-20220407164153438](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407164153438.png)

## Semaphore用于有限的资源，比如数据库的连接数![image-20220407164712869](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407164712869.png)![image-20220407165012715](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407165012715.png)![image-20220407170717385](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407170717385.png)![image-20220407170858635](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407170858635.png)![image-20220407173908302](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407173908302.png)![image-20220407173846043](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407173846043.png)

## StampedLock乐观锁，对性能是个提升，提高了吞吐量（特别是在读线程）![image-20220407174309947](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407174309947.png)![image-20220407174357866](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407174357866.png)

综上，竞争者少时用synchronized(不会造成死锁)，多时用reentrantLock（会造成死锁）

![image-20220407174911843](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407174911843.png)![image-20220407175341271](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407175341271.png)![image-20220407175454283](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407175454283.png)![image-20220407175552454](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407175552454.png)

# 第8章 JUC组件拓展![image-20220407182531722](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407182531722.png)![image-20220407202649031](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407202649031.png)![image-20220407203316144](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407203316144.png)![image-20220407203359330](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407203359330.png)![image-20220407203521664](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407203521664.png)![image-20220407204509504](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407204509504.png)![image-20220407204909416](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407204909416.png)

# 第9章 线程调度-线程池

![image-20220408132449908](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408132449908.png)![image-20220408132548123](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408132548123.png)![image-20220408132737630](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408132737630.png)

## 节省CPU、操作系统、环境切换开销：设置较大队列和较小线程池![image-20220408133630841](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408133630841.png)![image-20220408171511219](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408171511219.png)![image-20220408171603286](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408171603286.png)![image-20220408171946652](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408171946652.png)![image-20220408172204991](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408172204991.png)![image-20220408172350408](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408172350408.png)![image-20220408173107698](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408173107698.png)![image-20220408173212198](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408173212198.png)![image-20220408173628883](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408173628883.png)![image-20220408173649218](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408173649218.png)

## 重要：线程池配置

# ![image-20220408173750391](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408173750391.png)![image-20220408173955276](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408173955276.png)第10章 多线程并发拓展

![image-20220408174315015](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408174315015.png)

## 避免死锁：1、注意代码顺序2、加锁过期时间3、死锁检测（用代码实现，较难，顺序，线程优先级）4、记好日志![image-20220408175641676](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408175641676.png)![image-20220408175834509](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408175834509.png)![image-20220408175935392](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408175935392.png)![image-20220408200408765](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408200408765.png)![image-20220408200520343](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408200520343.png)

![ ](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\12.jpg)





![13](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\13.jpg)

![14](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\14.jpg)

![15](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\15.jpg)

![16](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\16.jpg)

## 综上，HashMap在rehash时容易出现死循环

![image-20220408202048939](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408202048939.png)

## fast-fail:使用迭代器过程中，HashMap被修改了，抛出ConcurrentModificationException（HashMap并发修改异常），可以使用① new ConcurrentHashMap<>();

## ②Collections.syncronizedMap(new HashMap())来解决

![image-20220408202722021](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408202722021.png)

## JDK7用分段锁，Segment继承自ReentrantLock

都是Key的Hash值与数组长度取模确定Key在数组中的索引

![18](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\18.jpg)![image-20220408203431858](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408203431858.png)

# 第11章 高并发处理思路与手段

![image-20220408221444736](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408221444736.png)![image-20220408222043302](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408222043302.png)

## 写操作扩展一般是水平扩容容易的，如Cassandra、Hbase等，因为单个机器扩展有限

# 第12章 高并发之缓存思路

![19](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\19.jpg)![image-20220408222822228](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408222822228.png)![image-20220408223546225](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408223546225.png)![image-20220408223618188](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408223618188.png)

![image-20220408224429028](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408224429028.png)

![21](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\21.png)

![22](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\22.png)

![23](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\23.png)![image-20220408233718563](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408233718563.png)

![24](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\24.png)

![image-20220408233818422](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408233818422.png)

![image-20220408233917271](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408233917271.png)

# ![image-20220408234126733](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408234126733.png)![image-20220408234245679](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408234245679.png)![image-20220408234741512](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220408234741512.png)第13章 高并发之消息队列思路

![image-20220409112121718](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409112121718.png)![image-20220409112418599](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409112418599.png)![image-20220409112611332](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409112611332.png)![image-20220409113824626](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409113824626.png)![image-20220409113836308](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409113836308.png)

# ![28](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\28.png)![image-20220409114242322](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409114242322.png)![image-20220409114534783](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409114534783.png)![image-20220409114755595](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409114755595.png)第14章 高并发之应用拆分(系统拆分)思路![image-20220409120735850](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409120735850.png)![image-20220409121722254](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409121722254.png)![image-20220409122136993](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409122136993.png)![image-20220409122222391](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409122222391.png)

![29](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\29.png)

## dubbo和webService都是服务框架，但只有dubbo是分布式服务框架，webService需要结合其它组件来实现负载均衡，dubbo支持软负载均衡,Registry一般用ZooKeeper![image-20220409123614955](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409123614955.png)

![30](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\30.png)

## 同步调用的两种方式：REST和RPC

# 第15章 高并发之应用限流思路

![31](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\31.png)

![image-20220409161052354](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409161052354.png)![image-20220409161151907](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409161151907.png)

![32](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\32.png)

![33](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\33.png)

## 计数器法也是一种滑动窗口，只是没进一步细分

![34](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\34.png)

## 漏桶、令牌桶天生不会出现临界问题

# ![35](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\35.png)![image-20220409162251584](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409162251584.png)第16章 高并发之服务降级与服务熔断思路

# ![image-20220409162632741](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409162632741.png)![image-20220409163032909](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409163032909.png)![image-20220409163049179](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409163049179.png)![image-20220409163120749](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409163120749.png)![image-20220409163157352](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409163157352.png)![image-20220409163229274](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409163229274.png)![36](D:\咕泡3\Java并发编程入门与高并发面试\Java并发课程资料\Java并发课程资料\相关图例\36.png)

# 第17章 高并发之数据库切库分库分表思路![image-20220409163428481](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409163428481.png)![image-20220409163605588](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409163605588.png)![image-20220409163635087](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409163635087.png)![image-20220409163757318](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409163757318.png)![image-20220409163814864](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409163814864.png)![image-20220409164245646](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409164245646.png)

# 第18章 高并发之高可用手段介绍![image-20220409164758656](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409164758656.png)![image-20220409164849509](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409164849509.png)第19章 课程总结

![image-20220409165015925](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409165015925.png)![image-20220409165130007](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409165130007.png)![image-20220409165315800](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409165315800.png)![image-20220409170431715](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409170431715.png)![image-20220409170610208](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220409170610208.png)



