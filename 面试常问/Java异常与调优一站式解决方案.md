![image-20220404082839341](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220404082839341.png)

![image-20220404225552640](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220404225552640.png)

![image-20220404230420192](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220404230420192.png)

![image-20220404231020704](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220404231020704.png)

![image-20220404231245473](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220404231245473.png)

# 栈是连续的内存区域，java默认的栈空间是1M，超过报栈溢出。每个线程有自己的栈空间

![image-20220404231813522](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220404231813522.png)

![image-20220404232024238](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220404232024238.png)

![image-20220404232214926](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220404232214926.png)

![image-20220404234219990](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220404234219990.png)

![image-20220404234937661](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220404234937661.png)

![image-20220405000500858](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405000500858.png)

![image-20220405000530574](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405000530574.png)

![image-20220405000645243](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405000645243.png)

# ![image-20220405000659878](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405000659878.png)第3章 Java 异常处理的基本原则

![image-20220405094730017](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405094730017.png)

![image-20220405095122122](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405095122122.png)![image-20220411094306839](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411094306839.png)![image-20220411094620080](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411094620080.png)

## 3-3 自定义异常和标准异常到底应该怎么选

# ![image-20220411094841409](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411094841409.png)![image-20220411095314922](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411095314922.png)

## 3-5 异常可以被忽略，但是要做到有理有据![image-20220411095713775](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411095713775.png)

## ![image-20220411100104358](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411100104358.png)比如几千万条数据的大文件，都传90%，一个异常过来白传了

## ![image-20220411100333908](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411100333908.png)3-6 尽最大的努力保证异常不影响系统的状态![image-20220411100850820](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411100850820.png)

## ![image-20220411101300616](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411101300616.png)final是对象的内存地址不可变，但是属性可变![image-20220411101539622](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411101539622.png)![image-20220411101815252](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411101815252.png)![image-20220411102029464](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411102029464.png)![image-20220411102224441](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411102224441.png)

副本大了会浪费内存和性能！回滚难度太高！![image-20220411102410831](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411102410831.png)

综上，最推荐的是提前检查参数有效性和调整计算中的顺序

## 3-7 回顾下我们该怎么处理异常

![image-20220411102718622](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411102718622.png)

## 3-9 里程碑：关于异常的一切

![image-20220411103456431](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411103456431.png)

# ![image-20220411103809937](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411103809937.png)![image-20220411103925392](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411103925392.png)第4章 深入理解 Java 日志框架体系

## 4-2 SLF4J 和 JCL 是怎么绑定日志实现的

![image-20220411114603118](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411114603118.png)![image-20220411114640959](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411114640959.png)![image-20220411115044657](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411115044657.png)

## ![image-20220411120344217](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411120344217.png)![image-20220411121123298](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411121123298.png)![image-20220411121800695](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411121800695.png)4-4 Log4j2 基础：学会使用它（搞懂配置并应用)

![image-20220411122838924](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411122838924.png)![image-20220411154700612](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411154700612.png)

## ![image-20220411155445435](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411155445435.png)![image-20220411155631650](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411155631650.png)![image-20220411155753254](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411155753254.png)4-6 Log4j2 进阶：它是怎样工作的

![image-20220411155925240](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411155925240.png)![image-20220411160958209](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411160958209.png)![image-20220411162053942](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411162053942.png)![image-20220411162805458](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411162805458.png)![image-20220411163004271](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411163004271.png)![image-20220411165227579](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411165227579.png)

# ![image-20220411165646141](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411165646141.png)![image-20220411165854490](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411165854490.png)

## 综上，加了注解的代码可以去看class!![image-20220411170002660](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411170002660.png)![image-20220411170452963](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411170452963.png)![image-20220411170108017](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411170108017.png)![image-20220411170255809](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411170255809.png)

# 第5章 优良的日志记录需要遵循一定的规范

![image-20220411171650735](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411171650735.png)

# ![image-20220411175625610](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411175625610.png)![image-20220411175711079](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411175711079.png)![image-20220411183822633](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411183822633.png)![image-20220411183854334](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411183854334.png)![image-20220411184136477](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411184136477.png)![image-20220411185454340](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411185454340.png)![image-20220411185848429](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411185848429.png)![image-20220411191349001](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411191349001.png)![image-20220411191853973](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411191853973.png)![image-20220411212258223](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411212258223.png)![image-20220411213749996](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411213749996.png)![image-20220411213902515](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411213902515.png)![image-20220411214240428](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411214240428.png)![image-20220411214930332](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411214930332.png)![image-20220411215259334](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411215259334.png)![image-20220411230757127](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411230757127.png)![image-20220411231007259](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411231007259.png)![image-20220411231121351](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411231121351.png)![image-20220411231244350](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411231244350.png)![image-20220411231711125](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220411231711125.png)第6章 彻底掌握 Intellij IDEA 的代码调试

![image-20220405173149351](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405173149351.png)

![image-20220405173239616](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405173239616.png)

![image-20220405173651124](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405173651124.png)

![image-20220405205423879](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405205423879.png)

![image-20220405213250653](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405213250653.png)

![image-20220405213722302](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405213722302.png)

![image-20220405213803380](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405213803380.png)

![image-20220405213834233](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405213834233.png)

![image-20220405213924485](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405213924485.png)

![image-20220405214120785](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405214120785.png)

![image-20220405214205564](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405214205564.png)

![image-20220405214826942](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405214826942.png)

# 第7章 学会分析 Java 线程堆栈

![image-20220405215429775](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405215429775.png)

![image-20220405215813102](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405215813102.png)

![image-20220405215925849](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405215925849.png)

![image-20220405231209841](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220405231209841.png)

![image-20220406111526465](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220406111526465.png)

![image-20220406121129423](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220406121129423.png)

![image-20220406121557162](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220406121557162.png)

![image-20220406124218992](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220406124218992.png)

![image-20220406124327806](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220406124327806.png)

![image-20220406124838164](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220406124838164.png)

![image-20220406211507500](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220406211507500.png)

![image-20220406211912104](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220406211912104.png)

![image-20220406211943485](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220406211943485.png)

![image-20220406212119904](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220406212119904.png)

## 一般来说，超过100个WAITING线程就不好了

![image-20220406225831771](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220406225831771.png)

![image-20220406230230372](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220406230230372.png)

![image-20220406230308250](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220406230308250.png)

![image-20220406230422640](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220406230422640.png)

![image-20220406230522867](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220406230522867.png)

## 重要：上面四种已经涵盖95%堆栈问题的场景

# 第8章 理解并学会 JVM 性能调优

![image-20220407093351146](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220407093351146.png)

架构调优、代码调优、JVM调优（只有当架构调优和代码调优已经不能再调了才用）、数据库调优、操作系统调优

![image-20220412091421876](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220412091421876.png)

![image-20220412091635859](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220412091635859.png)

![image-20220412091651880](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220412091651880.png)

![image-20220412092021880](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220412092021880.png)

![image-20220412092130261](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220412092130261.png)

![image-20220412092841912](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220412092841912.png)

![image-20220412093224248](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220412093224248.png)

![image-20220412093052394](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220412093052394.png)

![image-20220412093344021](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220412093344021.png)

![image-20220412095055085](C:\Users\kgliu\AppData\Roaming\Typora\typora-user-images\image-20220412095055085.png)
