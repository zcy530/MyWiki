## 数据库系统概念三 | 数据存储和查询

zcy 2021/6/25



## 第十章 存储和文件结构

#### 10.1存储设备基础

（属性、排序、效率、在整个体系架构里的位置）

高速缓冲存储器>主存储器>快闪存储器>磁盘>光盘>磁带

#### 10.2 磁盘部分的概念

（11章12章会涉及）

扇区section 磁道track 读写头 read-write head 

磁盘臂 disk arm 柱面 cylinder

扇区是从磁盘读出和写入信息的最小单位

RAID：独立磁盘冗余阵列

作用：通过冗余提高可靠性（奇偶校验），通过并行提高性能

磁盘性能的度量：访问时间，寻道时间，平均寻道时间，数据传输率，平均故障时间

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210626144000227.png" alt="image-20210626144000227" style="zoom: 67%;" />

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210626144034358.png" alt="image-20210626144034358" style="zoom: 67%;" />

#### 10.5 文件组织 

定长记录：

变长记录：分槽的页结构

#### 10.6 文件中记录的组织

堆文件组织 顺序文件组织 散列文件组织



## 11章 索引与散列

#### 11.1 基本概念

顺序索引

散列索引

![image-20210626145041944](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210626145041944.png)

![image-20210626145059102](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210626145059102.png)

![image-20210626145132100](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210626145132100.png)

![image-20210626145303445](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210626145303445.png)

![image-20210626150131687](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210626150131687.png)



#### :star:11.2 顺序索引

- 主索引和辅助索引 primary index/secondary index

  又叫聚集索引和非聚集索引 clustering index/nonclusering  index

  包含记录的文件按照某个搜索码指定的顺序排序，该搜索码对应的索引成为聚集索引

  搜索码指定的顺序与文件中记录的物理顺序不同的索引成为非聚集索引

  ![image-20210626160452042](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210626160452042.png)

  ![image-20210626161818964](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210626161818964.png)

  ![image-20210626162236820](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210626162236820.png)

  

- 稠密索引和稀疏索引 dense index/sparse index

  稠密索引：文件中每个搜索码值都有一个索引项

  稀疏索引：只为搜索码的某些值建立索引项，只有索引是聚集索引（当关系按照搜索码排列顺序存储时）才能使用稀疏索引

  ![image-20210626155857159](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210626155857159.png)

  ![image-20210626160036400](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210626160036400.png)

  ![image-20210626160135095](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210626160135095.png)



11.3也是重点 b+树 基本组成 结构 在查询里面的作用 怎么插入删除节点 （考察重点）::star:

![image-20210626163331250](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210626163331250.png)

![image-20210626163551482](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210626163551482.png)

![image-20210626163753283](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210626163753283.png)

![image-20210626164013790](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210626164013790.png)



插入节点

![image-20210626165031084](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210626165031084.png)

![image-20210626170858237](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210626170858237.png)

![image-20210626171034133](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210626171034133.png)

11.4 不过多考察

hash部分跳过







## 第12章 查询处理 

首先了解基本概念 为什么要做查询处理 实际上是对应怎么去磁盘取数据

#### 12.1 概述

代价取决于两个因素：执行的算法、数据库目录中的统计信息估计成本

#### 12.2 查询代价 Query Cost

查询处理的代价包括：磁盘存取，执行一个查询所需要的CPU时间，在并行/分布式数据库系统中的通信代价



用传送磁盘块数以及搜索磁盘次数来度量查询计划的代价：

假设瓷盘子系统传输一个块的数据平均消耗t_T秒，磁盘平均访问时间（磁盘搜索时间+旋转延迟）为t_S秒，则一次传输b个块，以及执行S次磁盘搜索的操作将消耗（b*t_T+S*t_S）秒。
其中t_T和t_S必须针对所使用的磁盘系统来计算



通果把读磁盘块和写磁盘块区分开，可以进一步细化磁盘存取代价的估算。

本书给出的代价没有包括将操作最终写回磁盘的代价，当需要时需要单独考虑。

- 本书所考虑的算法代价依赖于主存中缓冲区的大小

- 最好的情形是所有的数据都可以读入到缓冲区中，不必再访问磁盘

- 最坏的情形是假定缓冲区只能容纳数目不多的块——大约每隔关系一块

- 在代价估算时，通常假定最坏的情形

  

#### 12.3 选择运算

 表格有点问题： a3 a5要加一个传输 寻道时间

在b+树去做index，查到叶子节点，就是树的高度

后面算法的比较不过多涉及

复合查询有一些概念就好



#### 12.4排序 

外部归并排序 有个概念就好



#### 12.5 join

是重点 主要考察的是前几种





## 第13章 查询优化

主要考察前面几节

#### 13.1 概述

![image-20210627022738813](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210627022738813.png)

#### 13.2 关系表达式的转换

等价转换的规则

13.3 根据统计信息做估计 （不特别明确的考察但是大家要有概念）

有时候带有比较大的误差 不明确考察但是要有概念

后面跳过



## 第14章 事务 transaction

#### 14.1 概念

构成单一逻辑工作单元的操作集合称作事务

事务是访问并可能更新各种数据项的一个执行单元

事务调度 schedule：一组事务的基本步（读写、锁解锁）的一种执行顺序称为对这组事务的一个调度



ACID property：

原子性 atomicity

隔离性 isolation

持久性 durability

一致性 consistency



#### 14.4 生命周期

活动的 active：初始状态

部分提交的 partially committed：最后一条语句执行后

失败的 failed：发现正常的执行不能继续后

中止的 aborted：事务回滚并且数据库已恢复到事务开始执行前的状态后

提交的 committed：成功完成后



#### 14.6 可串化 

冲突可串化 conflict serializability

当i，j是**不同事务在相同的数据项上**的操作，并且其中至少有一个是write指令，则IJ是冲突的

**冲突等价** conflict equivalent：如果调度S可以经过一系列非冲突指令交换转换成S‘，我们称S与S’是冲突等价的

**冲突可串行化** conflict serializability：如果调度S与一个串行调度冲突等价，则称调度S是冲突可串行化的

满足冲突可串行性，一定满足可串行性，反之不然

**优先图** precedence graph （前驱图）

每个事务是一个节点，每个有冲突的操作是一条边，如果没有环就是冲突可串行化的

![image-20210627164445818](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210627164445818.png)

![image-20210627165738126](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210627165738126.png)



14.7以后都是概念为后面做准备

14.8 不考察14.9 14.10也



## 第15章 并发控制

#### 15.1 加锁协议

共享的shared S

排他的 exclusive X

可以让多个事务读取一个数据项但是限制同时只能有一个事务进行写操作

相容函数 compatibility function 

封锁协议 locking protocol：规定事务何时对数据项们进行加锁、解锁，限制了可能的调度数目

![image-20210627190307282](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627190307282.png)

![image-20210627190556072](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627190556072.png)

![image-20210627190834667](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627190834667.png)



**两阶段封锁协议 two-phase locking protocol**

要求每个事务分成两个阶段提出加锁和解锁的申请

1.增长阶段 growing phase 事务可以获得锁，不能释放锁

2.缩减阶段 shrinking pahse 事务可以释放锁，不能获得新锁

保证了冲突可串行化

严格两阶段封锁协议：所有排他锁必须在事务提交后方可释放

强两阶段封锁协议：要求事务提交之前不得释放任何锁

![image-20210627191058994](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627191058994.png)



#### 15.2 死锁处理

1.通过对加锁请求进行排序或要求同时获得所有的锁来保证不会发生循环等待

2.每当等待有可能导致死锁，进行事务回滚而不是等待加锁

#### 15.3 多粒度

怎么在并发调度里面加锁

死锁的概念

两个阶段的加锁协议（必考）

锁的实现看一看就好

graphbase协议不考了

死锁处理知道概念就好

等待图

#### 15.4 时间戳

![image-20210627210643847](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627210643847.png)

![image-20210627210801356](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627210801356.png)

![image-20210627210940003](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627210940003.png)



## 第16章 恢复系统

#### 16.1 概念

恢复算法是出现故障时确保数据库一致性、事务原子性和持久性的技术

故障分类

transaction failure，system crash，disk failure

存储器

volatile storage

nonvolatile storage

stable storage



#### 16.3 恢复与原子性

使用数据库的两种方法

deferred database modification 延迟的数据库修改

immediate database modification 立即的数据库修改



![image-20210627223108583](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627223108583.png)

![image-20210627223222533](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627223222533.png)

![image-20210627223456516](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627223456516.png)

![image-20210627223957791](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627223957791.png)

![image-20210627224028465](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627224028465.png)

![image-20210627224101587](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627224101587.png)

![image-20210627224243696](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627224243696.png)

![image-20210627224255110](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627224255110.png)

![image-20210627224450181](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627224450181.png)

![image-20210627224616684](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627224616684.png)

![image-20210627224721396](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627224721396.png)





undo/redo

![image-20210627225343899](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627225343899.png)

![image-20210627225431853](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627225431853.png)

![image-20210627225442475](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210627225442475.png)

16.4 肯定要重点考察

16.5 之后涉及到buffer情况 修正 了解就行 不做重点考察的内容

这一章比较简单