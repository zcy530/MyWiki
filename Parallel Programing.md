## Parallel Programing

caiyi 2021/6/17



## 第一章

#### 1.为什么要构建并行系统?

电路晶体管密度过大会使处理器能耗增加，散热的问题使通过继续增快集成电路密度提高处理器性能不再现实，因此集成电路商决定构建多核处理器。

#### 2.为什么要编写并行程序？

之前的串行程序适合之前的传统处理器，为了充分发掘多核处理器的性能，必须对常见串行结构进行并行化以提高性能。

#### 3.如何编写并行程序？

基本思想是把任务分配给各个核，主要有两种方法：任务并行和数据并行。

**任务并行**指的是把各个的任务分配给不同的核

**数据并行**指的是将待处理的数据分配给各个核进行处理。

任务并行很可能每个核执行的任务不一样，数据并行分配给每个核的往往是相同的任务。

在并行计算中，需要注意协调过程，包括通信、负载平衡、同步

**通信**：在不同核把计算结果发送给其他核
**负载平衡**：每个核的计算的工作量应该大致相等
**同步**：同步每个核的运算时间

例子1：求累加的n项和
假设把数据分为n组分别累加，有一个接收数据累加和的变量x。正常情况下需要等变量的初始化在往其传数据。
如果变量还没初始化但其他的部分和已经送我来，会导致数据丢失等等。（没有同步的情况）
解决方案：写一个函数给他们一个同步函数（提出要求），让其他的核等，等x初始化后，在传数据（同步）

#### 4.怎么做？

利用消息传递接口（MPI）、POSIX线程和OpenMP来编写基本的并行程序

MPI和Pthread是C语言的扩展库，可以在C程序中使用扩展的类型定义、函数、宏，而OpenMP包含了一个扩展库以及对C编译器的部分修改

**共享内存系统**：各个核能够共享访问计算机的内存，可以通过检测和更新共享内存中的数据来协调各个核

**分布式内存系统**：每个核拥有自己的私有内存，核之间的通信是显式的必须使用类似在网络中发消息的机制

Pthreads和OpenMP是共享内存系统，MPI是分布式内存系统

![IMG_6751](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6751.PNG)

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210618181843501.png" alt="image-20210618181843501" style="zoom:67%;" />

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210618182150166.png" alt="image-20210618182150166" style="zoom:67%;" />

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210618182349637.png" alt="image-20210618182349637" style="zoom:67%;" />

#### 5. 并发、并行、分布式

并发（concurrent）：一个程序的多个任务在同一时间段内可以同时执行

并行（parallel）：一个程序通过多个任务协同工作去解决一个问题

分布式（distributed）：一个程序需要与其他程序协作解决一个问题

并行程序和分布式程序都是并发的

#### 6. 为什么实现并行程序很难

- Amdahl's Law 必须并行化大部分计算
- 数据局部性
- 通讯与同步
- 负载不平衡



## 第二章 并行硬件和并行软件

### 1.冯诺依曼结构

经典的冯诺依曼结构包括主存、中央处理单元（CPU）以及主存之间的互连结构（总线）

CPU分为控制单元和算术逻辑单元ALU

主存和CPU之间的分离叫做**冯诺依曼瓶颈**，互连结构限制了指令和数据访问的速率

![IMG_6752](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6752.PNG)

### 2.改进冯诺依曼结构

- #### **缓存 CACHE：**

  解决冯诺依曼瓶颈所使用的最广泛的方法之一

  缓存使一次访问能够传输更多的数据和指令，并且将部分代码和数据存在靠近CPU的特殊存储器里

  高速缓存器的访问时间比其他存储区域访问时间更短

  **局部性**：程序倾向于使用最近访问过的（时间局部性）和物理上接近存放的数据和指令（空间局部性）

  **高速缓存块/缓存行**：运用局部性原理，系统使用更宽的互联结构来访问数据和指令，一次内存访问能存取一整块的代码和数据，这些块称为高速缓存块。

  **缓存分层**：第一层最小但最快，高层更大但相对更慢

  **命中/缺失**：当向cache查询信息时，如果cache中有信息，则称为命中，如果信息不存在成为缺失

  读数据：如果发生cache缺失，处理器会阻塞直到高速缓存块从主存传送到cache中

  写数据：更新数据后，cache中的值与主存中的值不一致，有两种方法解决：写直达和写回

  ​               <u>写直达</u>：当CPU向cache写数据时，高速缓存会立即写入内存

  ​               <u>写回</u>：数据在缓存中被标记为脏数据，并在被新的缓存行替换时写回内存，回写缓冲区提高性能

  

  **高速缓存行应该存储在什么位置？**

  主存地址与Cache地址之间的转换是与主存块与Cache块之间的映射关系紧密联系

  **全相联**：每个高速缓存行能够放置在cache中的任意位置，主存中任何一块都可以映射到Cache中的任何一块

  优点：命中率较高，Cache的存储空间利用率高
  缺点：线路复杂，成本高，速度低

  <img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210618154143233.png" alt="image-20210618154143233" style="zoom:67%;" />

  **直接映射**：每个高速缓存行在cache中有唯一的位置，主存中的一个块只能映射到Cache的某一特定块中去，例如，主存的第0块、第16块、…、第2032块，只能映射到Cache的第0块；而主存的第1块、第17块、…、第2033块，只能映射到Cache的第1块

  优点：硬件简单，容易实现
  缺点：命中率低， Cache的存储空间利用率低

  <img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210618154119197.png" alt="image-20210618154119197" style="zoom: 67%;" />

  **n路组相联**：每个高速缓存行可以放置到cache中n个不同区域位置中的一个，是直接映射和全相联映射的折中方案，主存和Cache都分组，主存中一个组内的块数与Cache中的分组数相同，组间采用直接映射，组内采用全相联映射

  ![image-20210618154701903](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210618154701903.png)

  **替换策略：**

  直接映射：别无选择
  设置关联：首选无效条目
  LRU：选择最长时间未使用的
  随机的

  <img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210618171140530.png" alt="image-20210618171140530" style="zoom: 67%;" />

  

- #### 虚拟存储器：

  如果所有的指令和数据可能在主存中放不下，利用**虚拟内存**使主存作为辅存的缓存，将当前程序所需要的部分存放到主存，将暂时用不到的部分存储在辅存的块中，称为**交换空间**，通常成为**页**

  使用**页表**来将虚拟地址转为物理地址，但这样使访问内存的次数增加，所以使用虚拟地址来计算出物理地址，而不用访存。页表的缺点是会使访问主存区域时间加倍，为了解决页表对性能的负担，处理器使用**TLB（转译后备缓冲区）**减少对主存的访问。

  ![IMG_6753(20210618-171800)](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6753(20210618-171800).PNG)

  TLB在快速存储介质中缓存了一些页表的条目，大部分存储器所访问页的物理地址已经存储在TLB中了，对主存中页表的访问可以大大减少

  **TLB命中/缺失：**当查询的地址和虚拟页号在TLB中，成为命中

  **页面失效**：想要访问的页不在内存中，即页表没有合法的物理地址，只存储在磁盘上

  

  <img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/07163541_gEDQ.png" alt="architecture" style="zoom:50%;" />

- #### 指令级并行

  **指令级并行ILP**：通过让多个处理器部件或者功能单元同时执行指令来提高处理器性能，主要有两种方式：流水线和多发射。
  **流水线**：将功能分成多个单独的硬件或者单元，并把他们按顺序串接来提高性能

  **多发射**：通过复制功能单元来同时执行程序中的不同指令

  <img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6754.PNG" alt="IMG_6754" style="zoom:67%;" />

  指令级并行通常很难利用，因为程序中还有很多部分有依赖关系

  线程级并行TLP、硬件多线程、同步多线程都能提高并行性。





### 3. 并行硬件

能够通过修改源代码而开发并行性或者必须修改源代码来开发并行性，叫并行硬件。

- #### SIMD系统

  Fylnn分类法对计算机体系进行分类，根据同时能管理的指令流数目和数据流数目来对系统分类

  **单指令单数据流（SISD）**：一次执行一条指令，一次存取一个数据项，冯诺依曼体系

  **单指令多数据流（SIMD）**：并行系统，他通过对多个数据执行单一指令从而实现在多个数据流上的操作。可以看做是一个处理单元有一个控制单元和多个ALU。

- #### MIMD系统

  **多指令多数据流（MIMD）**：支持同时多个指令流在多个数据流上操作，可以看做一组完全独立的处理单元且每个处理单元都有一个控制单元和一个ALU

  **共享内存是隐式通信，分布式内存是显式通信**

  分布内存系统：每个处理器有自己私有的内存空间，处理器-内存通过互联网络通信

  共享内存系统：一组自治的处理器通过互联网络，与内存系统相互连接， 每个处理器能够访问内存区域

  ​		一致内存访问UMA：每个核访问内存中任意一个区域的时间都相同

  ​		非一致内存访问NUMA：访问与核直接链接的那块内存区域更快

  <img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210618185104435.png" alt="image-20210618185104435" style="zoom:67%;" />

  

- #### 互联网络

  ==**共享互连网络：**==共享内存系统中，最常用总线和交叉开关矩阵

  **总线**由一组并行通信线和控制对总线访问的硬件组成

  优点是成本低和灵活，缺点是设备多的话会经常争夺总线，降低性能。

  **交叉开关矩阵**使用交换器来控制设备间数据传递。它允许不同设备间的同时通信，但是开销相比总线更大。

  <img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210618201230528.png" alt="image-20210618201230528" style="zoom:67%;" />

  <img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210618201714767.png" alt="image-20210618201714767" style="zoom:67%;" />

  ==**分布式内存互联网络**==

  **直接互连**：每个交换器直接连接到处理器-内存对，并且交换器之间相互连接。

  **间接互连**：交换机可能不会直接连接到处理器。间接网络中相对简单的例子：交叉开关网络和omega网络

  通常显示为单向链路和一组处理器，每个处理器都有一个传出和传入链路，以及一个交换网络

  互连的成本可能是机器的很大一部分，由以下因素控制：链接数、开关数量、可用带宽

  ![IMG_6765](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6765.PNG)

  

  ![IMG_6764](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6764.PNG)

  

  

  **等分宽度**：“同时通信的数量”或“连接性”的度量。它计算网络分为一半一半后两部分间可同时<u>发生的通信数</u>

  **等分带宽**：网络质量的衡量标准。它不计算加入两半的链路数量，而是对<u>链路的带宽求和</u>。

  ![IMG_6761](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6761.PNG)

  ![IMG_6762](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6762.PNG)

  在多核系统中，每个核都有自己的存储空间，储存相同变量的副本，当一个处理器修改自己的副本时，应该令其他处理器知道该变量已经更新。

  

  与内存系统一样，我们也在消息传递中考虑带宽和延迟

  ![image-20210618202735398](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210618202735398.png)

  

- #### Cache一致性

  有两种主要方法保证cache一致性：监听Cache一致性协议和基于目录的Cache的一致性协议。前者是利用互连网络对更新行为进行广播，后者是通过使用一个叫目录的结构来标记更新状态。

  <img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210618183724738.png" alt="image-20210618183724738" style="zoom:67%;" />

  <img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210618183924867.png" alt="image-20210618183924867" style="zoom:67%;" />

  <img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210618184045536.png" alt="image-20210618184045536" style="zoom:67%;" />

  <img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210618184335700.png" alt="image-20210618184335700" style="zoom:67%;" />

### 4. 性能计算

**Some definitions:**
Token : A group of inputs processed to produce a group of outputs
Latency : Time for one token to pass from start to end
Throughput : The number of tokens that can be produced per unit time

### 5. 并行算法

竞争：当执行结果取决于两个或多个事件的时间时，存在竞争条件

数据依赖：对必须保留以保持正确性的一对内存操作的排序

同步：用于对线程之间的控制进行排序或对并行代码中的数据访问进行排序

原子性：一组操作是原子的，如果它们同时执行或都不执行。 因此，无法查看部分执行的结果

互斥：最多有一个线程可以随时执行代码



互斥锁的方法有**锁争用和粒度差**的缺点

如何增加并行粒度：每个线程使用它自己的私有变量，并独立于其他内核执行此代码块。

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210619125107851.png" alt="image-20210619125107851" style="zoom:67%;" />



任务并行性：将解决问题的各种任务划分到内核之间。
数据并行：在核心之间划分用于解决问题的数据，每个核心对其数据的一部分执行类似的操作

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210619125317262.png" alt="image-20210619125317262" style="zoom:67%;" />

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210619125332670.png" alt="image-20210619125332670" style="zoom:67%;" />

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210619125622880.png" alt="image-20210619125622880" style="zoom:67%;" />



总结：如何导出顺序算法的并行版本

1. Computation Partitioning  计算分区
2. Preserving Dependences using Synchronization 使用同步保留依赖关系
3. Reduction Computations减少计算
4. Overheads费用

四个步骤设计一个并行程序：

1. 将问题的解决方案划分成多个任务
2. 在任务间识别出需要的通信信道
3. 将任务聚合成复合任务
4. 在核上分配复合任务

### 6. 数据依赖

定义：如果两个内存访问可能引用相同的内存位置并且其中一个引用是写操作，则它们涉及数据依赖

数据依赖是对必须保留以保持正确性的一对内存操作的排序
数据依赖可以在两个不同的程序语句之间，也可以在同一程序语句的两个不同的动态执行之间

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210619130914838.png" alt="image-20210619130914838" style="zoom:67%;" />

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210619131534822.png" alt="image-20210619131534822" style="zoom:67%;" />

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210619131554728.png" alt="image-20210619131554728" style="zoom:67%;" />

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210619131822216.png" alt="image-20210619131822216" style="zoom:67%;" />

### 7. 习题解答



## 第四章 Pthreads

### 1.介绍

#### **共享内存编程**（线程）

​		启动单个进程和 fork 线程

​		线程执行工作

​		线程通过==共享内存==进行通信

​		线程通过同步（也通过共享内存）进行协调

#### **分布式内存编程**（进程）

​		在多个系统上启动多个进程

​		流程执行工作

​		进程通过==消息传递==进行通信

​		进程通过消息传递或同步（生成消息）进行协调

#### 动态线程

有一个主线程，并且在任何给定时刻都有一个(可能是空的)工作线程集合。

主线程通常等待工作请求，当一个新的请求到达时，它会fork一个工作线程，该线程执行请求，当该线程完成工作时，它终止并加入主线程。

这种范例有效地利用了系统资源，因为线程所需要的资源只在线程实际运行时才会被使用

#### 静态线程

在主线程进行任何必要的设置之后会fork出所有的线程，这些线程一直运行直到所有的工作完成。在线程加入主线程后，主线程可能会做一些清理(例如，释放内存)，这样被fork出来的线程也会终止。

在资源使用方面效率较低，如果一个线程是空闲的，它的资源都不能被释放。

优点是，它更接近于最广泛使用的分布式内存编程范例

#### 线程安全

如果一个函数或库在被多个同时执行的线程调用时能够“正确”操作，那么它就是线程安全的。

由于多个线程通过共享内存进行通信和协调，因此线程安全代码会使用适当的同步来修改共享内存的状态。

### 2.Pthread

POSIX: Portable Operating System Interface for UNIX，是UNIX的可移植操作系统接口

PThreads: POSIX线程接口。系统调用来创建和同步线程

PThreads支持创建并行性、同步，但不支持显式通信，因为共享内存是隐式的

