# OOAD



zcy 2021/9/25



# 第三章 面向对象分析



领英一键投递

招聘官网

## 1. 基本概念

面向对象开发需要掌握的极为重要的能力：为软件对象分配职责

方法：职责驱动的设计，遵循GRASP原则

面向对象分析OOA：发现并描述问题领域里的对象或者概念（概念类）

面向对象设计OOD：定义软件对象、以及它们之间如何协作完成功能的（设计类）

基本过程：定义用例->定义领域模型->定义交互图->定义设计类图



领域模型（概念模型、领域对象模型、分析对象模型）：问题领域的概念类以及真实对象的可视化表示

![image-20210925144943488](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925144946.png)



低表示差异（LRG）：概念类可以作为软件类，区别是概念类没有操作，软件类有操作。就是说领域模型里面很多的概念类在我们设计的时候可以直接拿来用

## 2. 面向对象分析方法

系统开发有两种主要的分析方法：面向功能的分析（抽象层面）、面向对象的分析（模块层面）

面向对象分析与结构化分析方法之间的最大差异是：前者根据对象划分系统，而后者根据功能 

面向对象分析主要步骤：识别对象 → 组织对象 → 定义对象之间的关系 → 定义对象的操作（在设计阶段完成）→ 定义对象内部细节

**面向对象分析的三种方法：名词法（Conceptual model）、分析模型（Analysis model with stereotypes）、CRC cards**



### 2.1 名词法案例：

一般user ➡️ user pannel

可能的抉择：一个名词，是作为概念类合适，还是作为某个类的属性更合适？

![image-20210925160406820](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925160408.png)

![image-20210925160420792](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925160435.png)

![image-20210925160717565](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925160719.png)



### 2.2 分析模型法案例：

一个健壮、稳定的模型，必须与实现环境无关，实现环境的任何变化，不会影响到系统的逻辑结构

分析模型能够关注到系统的**信息、行为、展示（输入/输出）三个维度**的特性

![image-20210925161241213](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925161243.png)



分析模型用到三种符号：实体（自身的功能运算存储等）、边界（跟用户打交道输入输出）、控制类（资源调度）

![image-20210925161328397](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925161330.png)

![image-20210925161425419](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925161426.png)

上面废品回收机的例子：

- 接口对象

![image-20210925161852695](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925161855.png)

- 实体对象

![image-20210925161913503](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925161915.png)

- 控制对象

![image-20210925161932710](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925161934.png)



### 2.3 CRC方法标识概念类

CRC stands for：class 类、responsibilities 职责、collaborations协作

CRC索引卡片格式：左边是类和职责，右边是协作类以及父类子类

![image-20211012090222858](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211012090225.png)

CRC特点：非正式的，不是很细节的，需要进一步精化

一个简单的例子：分析绘图工具软件

![image-20211012091313718](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211012091330.png)

![image-20211012093110566](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211012093113.png)

为了寻找crc我们引入了两个技术：头脑风暴，角色扮演

CRC案例

1.需求描述

2.列出概念类

3.标识核心概念类：关键的，无关的，待定的

4.明确系统范围

5.去掉不必要的核心类，辨析一个概念是属性还是类（它不做具体的事情，它不能改变状态）

6.为核心类分配职责

## 3. 面向对象设计

在概念模型的基础上进行设计

**低表示差异**（Low Representation Gap）：概念模型里面的<u>概念类</u>和设计模型里面的<u>设计类</u>，之间相似度很高差异很小



面向对象分析的主要核心思想：**职责驱动**

- 设计时考虑对象做什么、<u>或者知道什么</u>
- 一个对象对其他对象承担的义务或者合约
- 职责是一个对象的行为，而其他的对象依赖这种行为

**职责定义为两类**：

- <u>认知职责</u>：知道自己封装的私有数据、知道你和别人相关的数据、知道哪些是可以推导出来的数据
- <u>行为职责</u>：自己可以做什么、启动其他对象做事情、控制和协调其他对象的行为

![image-20210925162900793](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925162902.png)

废品回收机：

![image-20210925214228762](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210925214230.png)



## 4. 标识概念类和对象

面向对象分析的核心目的：发现对象、定义对象之间的关系

为了标识领域模型里的概念，我们有三种方法：名词法、分析模型法、crc



# 第五章 领域模型

## 1.领域模型图

没有定义操作的类图

包括：概念类、概念类关系、属性

理解概念类的三个层面：符号、内涵、外延

可以把描述性性质的概念单独作为概念类的情况：

1. 在数量很大的情况，不浪费存储空间

2. 如果删除对象的同时删除了描述，而该描述还需要继续维护

构建领域模型案例：

![image-20211019001722749](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019001731.png)

案例二大富翁游戏：

![image-20211019002020703](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019002021.png)



## 2.系统顺序图ssd

把待建系统看成黑盒子，研究参与者与系统边界的交互

SSD：System Sequence Diagram

![image-20211019003528882](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019003529.png)

![image-20211019002859485](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019002900.png)



系统顺序图与用例区别：

在一定程度上，系统顺序图与用例描述是对应的，只是系统顺序图更精炼，用例更详细，二者互为补充

系统顺序图和顺序图的区别：

顺序图强调的是系统内部，对象与对象之间如何分工协作

![image-20211019003614114](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019003615.png)



顺序图与代码

![image-20211019003733868](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019003735.png)



## 3.除了用例以外的需求信息

![image-20211019004340458](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019004341.png)

分类方法一：功能性需求和非功能性需求

分类方法二：FURPS+

![image-20211019004522393](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019004523.png)

![image-20211019004656560](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019004657.png)

# 第六章 从分析到设计

复习用例模型

![image-20211019005305395](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20211019005305395.png)

1. 参与者

![image-20211019005621278](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019005622.png)

2. 用例

![image-20211019005743063](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019005745.png)

## 6.3 契约式设计 dbc

design by contract

![image-20211019011609368](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019011610.png)

断言

![image-20211019011720678](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019011722.png)

定义一个前置和后置

![image-20211019011812920](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019011814.png)

形式化规格说明specification

![image-20211019012205449](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019012206.png)

类不变量 class invariant

![image-20211019012524182](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019012525.png)

操作契约

![image-20211019012925151](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019012926.png)

格式

![image-20211019013033472](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211019013034.png)





## 6.4 开始进入设计

**1.什么是架构**

架构是关于如何组织软件系统的一系列重大决策

- 如何选择组成系统的结构元素及接口
- 这些结构元素相互协作时的行为规范
- 这些结构元素如何组成逐渐变大的子系统

架构也称：逻辑架构/软件架构

不同于部署架构（deployment architecture）：定义这些结构元素分布在不同的物理设备上

**2.逻辑架构的设计方法**

分层法，  标识一定规模的结构元素

分层架构的优点：

- 各层都容易被替换
- 较低层次包含更多的操作细节，容易成为可重用构件
- 每层都容易分布部署与连接

*下层不要调用上层的功能！

![image-20211129203510214](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129203518.png)



## 6.5 面向对象设计

**面向对象设计**主要是在领域层（domin）的每个模块（module）里面，模块与模块之间，模块与层之间的关系，不属于面向对象分析和设计的范畴 

面向对象设计：领域层与ui层/数据层通过特定的接口进行通信

**model-view模式：**

model是领域层里面做的事情，计算数据存储等

view是界面，用户数据怎么传进来，怎么显示给用户看

**领域对象与设计对象的一致性**

领域模型中的payment是一个概念，在设计模型中是一个软件类，他们不是同一件事情，但前者启发了后者的定义，降低了表示差异

**从ssd（系统顺序图）到设计**

**职责驱动的设计（rdd）**

设计的总体思路就是职责驱动，标识职责，并把他们分配给不同的类 

职责分为行为职责doing和认知职责knowing 

软件对象只有方法，不能说职责

**GRASP原则**

面向对象设计的基本原则 grasp原则 

通用的职责分配软件原则 general responsibility assignment software principles

![image-20211129211335840](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129211338.png)



# 第七章 面向对象设计GRASP原则

## 7.1 创建者 creator

由谁来负责创建这个类的新实例

每项模式的格式：name、problem、solution

![image-20211129213754853](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129213757.png)

A和B都是软件对象，不是领域对象

创建模式有什么好处：对方的东西是可见的，高内聚，低耦合（我们两个一起做事情时不用跟别人创建联系）

## 7.2 信息专家 information expert

为一个对象分配职责的一般原则，这个对象拥有完成这个职责所必须的信息

![image-20211129214702342](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129214705.png)

information其实就是认知职责

信息专家的好处：封装性encapsulation，对象充分利用自身的信息，支持低耦合和高内聚，系统行为分不到不同的类

举例：

![image-20211129215322553](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129215325.png)



## 7.3 低耦合 low coupling

如何保证设计方案的依赖性、低的变化影响度、增加可重用性

**例子一 pos机计算总金额**

第一种解决方案，register创建了一个对象p，然后把这个对象的参数传给sale让他去用，相当于你朋友让你装修房子，你帮他喊了个装修队，把装修队的电话发给你朋友，但是你真的有必要知道这个p的信息吗，这就增加了系统的耦合关系

![image-20211129215904381](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129215908.png)

第二种解决方案

委托 delegate

register把任务委托给sale，sale去创建实例，减少了系统的耦合度

![image-20211129220147622](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129220149.png)

**耦合**：一个元素与其他元素的连接感知以及依赖程度的度量

**内聚和耦合的区别**：耦合（coupling）是模块与模块之间联系的强度，内聚（cohesion）是讲在模块内的操作之间的联系紧密的程度

根据信息专家得出来的方案支持低耦合的，它自己这一个类就已经具备了必要的数据和信息，所以它在做的时候就不需要去委托别人，自己就可以完成了，这样它跟外界的交流和依赖就变少了

![image-20211129221738004](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129221739.png)

低耦合支持类的相对独立，减少了变化带来的影响

与其他原则原则放在一起考虑，不要单独考虑低耦合，类与类之间没有耦合也不好

在继承关系中，子类和父类的耦合关系非常紧密。能用组合的地方不要用继承

可以耦合一些稳定的框架，比如java的包和库



## 7.4 控制器 Controller

在领域层，由谁负责首先接受并协调来自ui层的系统操作？因为ui层不应该包含任何逻辑，在ui上的系统操作必须传给领域层，由领域层来处理

领域层里面有一些类应该可以代表整个系统、子系统、或者这个设备

![image-20211129222619872](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129222621.png)

控制器有两类，一个是外观控制器，一个是会话session控制器

下图第一个是外观控制器，第二个是会话控制器

**外观控制器：**为子系统的一组接口提供一个一致的界面，当系统事件不是太多的时候，用一个外观控制器就可以了

**会话控制器：**是虚构出来的，领域模型没有这个概念。当我这个系统事件有很多是跟用例相关的，有好几组，建议每个组定义一个handler，哪个处理销售，哪个处理退货

![image-20211129222852538](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129222854.png)

**委托模式 delegation pattern**

外部输入事件可以来自参与者或者其他系统

facede相当于领域层对外部世界的脸

handler处理系统某个明确的功能集合，比如相关的一组系统事件

**控制器的优点**

容易适应ui的变化、领域层代码易于重用，有助于保证应用所需要的操作顺序

臃肿的控制器：bloated controller



## 7.5 高内聚 high cohesion

如何使对象功能专注、可理解、可管理、同时又支持低耦合？

方法：分配职责时保证高内聚

这也是一种理念，不具备可操作性，用作评价工具

![image-20211129224015092](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129224016.png)

**内聚的最佳实践：**

1. 一个对象完成的功能不要太多： 谁能保证任务重的对象在完成功能时不会引用到类外部的资源呢？（增加了耦合度）

2. 这些功能都是同一类别的 

![image-20211129224533133](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211129224534.png)

**类低内聚的症状：**

1. 做了许多相互无关的工作
2. 做了太多的工作

**类低内聚的原因：**

1. 太粒度的抽象
2. 做了太多本应该委托去其他类做的工作



## 7.6 多态 polymorphism

如何处理依据类型不同而有不同行为的一类需求，多态原则解决的问题是在职责分配时如何避免依据类型变化而进行不同的处理

![image-20211130020308943](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130020311.png)

多态案例

![image-20211130020628623](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130020633.png)



## 7.7 纯虚构 pure  fabrication

**problem：**如果依据信息专家原则获得的解决方案不合适，既不想违反低耦合、高内聚，也不想违反其他的原则，该如何把职责分配给对象（左右为难）

**solution：**把高度内聚的职责分配给人为虚构出来的一个类，这个类在领域模型里没有对应的概念。

这种方式在有的场合能起到支持低耦合高内聚、重用的效果

案例

![image-20211130022329551](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130022331.png)

![image-20211130022318405](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130022320.png)

纯虚构原则讨论

![image-20211130022425700](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130022427.png)



## 7.8 间接 indirection

若两个对象直接连接，导致耦合太近，如何解决？

problem：把职责分配到哪里可以避免两个或多个对象之间的直接耦合，如何解耦对象以保持较高的可重用性？

solution：把职责分配给一个中介对象，隔离对象与其他构建或者服务，使他们不产生直接耦合。因为中介对象使一种特殊的作用，一般对象与中间对象之间的直接耦合，相对比较简单

和纯虚构的区别：出发点不一样，间接是为了避免直接耦合，纯虚构是在低耦合高内聚都不能满足的时候要分配一个类出来，纯虚构这个类承担的职责是相对集中的，而中介相对来说要简单一点

![image-20211130062823035](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130062826.png)

##  7.9 隔离变化 protected variations

problem：需求一定会变化的，如何做到以系统的局部变化为代价就可以应对这一点。如何设计对象、系统和子系统，使得这些成分里面的变化因素、不稳定因素不会对系统的其余部分造成意想不到的影响

solution：标识出能够预计的变化或者不稳定点，职责分配的时候创建一个稳定的接口能把他们与系统的其余部分隔离开来

需要注意的两种可能的变化点：

![image-20211130063859861](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130063902.png)



# 第八章 其他原则

## 8.1 开闭原则ocp

软件系统应当允许功能扩展（开放性）

但是不允许修改原有的代码（即关闭性）

  ![image-20211130064858352](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130064901.png)

![image-20211130064834751](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130064838.png)

close不是绝对的，是战略性的，用到了隔离变化的思想

ocp的启发：

1. 定义所有的对象、数据为私有的

   涟漪效应 ripping effect

2. 不要使用全局变量  



![image-20211214081700691](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214081702.png)

## 8.2 组合 

能用组合的地方，不要用继承

![image-20211130065622893](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130065625.png)

**继承：**子类获得父系的全部功能，稍微调整一下，比如覆盖实现几个方法

继承的副作用：

1. 打破了封装性，父类和子类之间高度耦合
2. 继承的代码时静态/编译时绑定的
3. 客户需要购买整个软件包，花钱占内存
4. 父类定义了许多硬性规定，难以有个性化的东西 

**组合：**没有打破封装性

1. 对象组合是一种动态/运行时绑定

2. 整体与部分之间只有接口边界关联，耦合较低

3. 各部分职责明确

   每个对象清晰的集中在少量的任务上，容易独立测试



## 8.3 依赖倒置原则 dip

依赖太重就是耦合太近

:star:高层模块不应当依赖低层模块，两者都应该依赖抽象

:star:抽象不能依赖细节，细节应当依赖抽象

 ocp宣扬了目标，dip宣扬了一种机制 

![image-20211130071028489](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130071031.png)

![image-20211130071145776](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130071147.png)

在需求发生变化时是相对稳定的

启发：

1. 面向接口设计，而不是面向实现设计

   因为抽象类和接口修改的概率低，抽象概念容纳范围广，易于扩展/修改

2. 例外情况，类非常成熟稳定，再插入抽象层好处已经不多了，例如string class，这里就可以直接用具体类，不需要考虑依赖倒置

3. 避免依赖传递性

![image-20211130072134536](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211130072137.png)



## 8.4 可见性

对象之间的可见性
对于发送者对象向接收者对象发送消息，发送者必须对接收者可见
为了让对象 A 向对象 B 发送消息，B 必须对 A 可见。
发送者必须有某种指向接收者对象的引用或指针



可见性是一个对象“看到”或引用另一个对象的能力
四种常见方式
属性可见性
  B 是 A 的一个属性。
参数可见性
B 是 A 的方法的参数。
本地可见性
  B 是 A 的方法中的（非参数）本地对象。
全球知名度
  B 在某种程度上是全局可见的



实现局部可见性的两种常用方法
创建一个新的本地实例并将其分配给一个本地变量。
将方法调用的返回对象分配给局部变量



# 第九章 设计模式

## 9.3 工厂模式

面向抽象编程，不要面向具体实践

如果是面向接口的编程，我们可以隔离一些可能使得系统崩溃的变化。当代码需要使用很多具体的类时，增加新的具体类的时候，我们不得不修改代码。所以，我们的代码并不是“拒绝修改”的。如果要扩展新的具体类时，我们不得不重新打开代码进行修改

**问题**：又想new一个对象，又不知道对象在哪里，这个对象还没产生

**工厂模式的定义**：定义一个用于创建对象的接口，让子类决定实例化哪个子类。该模式把实例化延迟到其子类

![image-20211214084515504](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214084517.png)

**核心思想**：把变化集中起来

**例子**：披萨店生产不同的披萨

![image-20211214082954949](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214082956.png)

把上述代码改为工厂模式

![image-20211214082748120](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214082749.png)

![image-20211214082842421](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214082843.png)

![image-20211214082858297](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214082859.png)

总结一下上面这道题的意思

![image-20211214083103031](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214083104.png)

现在要在各个地方开分店，每个店的披萨保留老祖宗留下的操作，但允许一定的地方特色

需要一种机制将所有比萨制作活动“本地化”到 PizzaStore 类，同时让 Branchs 自由地拥有自己的区域风格

![image-20211214083749342](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214083750.png)

工厂模式的核心就是工厂函数，createPizza()就是工厂函数

![image-20211214083808027](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214083809.png)

子类该如何确定呢？

![image-20211214084143537](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214084145.png)

**抽象工厂模式：**工厂模式生产一样产品，抽象工厂模式生产一系列产品，一辆汽车所需要的多种产品，前门后门

![image-20211214085128284](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214085129.png)



## 9.4 命令模式

编程可用于控制房屋内设备的遥控器

**命令模式：**将一个请求封装成一个对象，从而能以不同的请求来参数化客户对象、把所有请求存入队列或者写入日志，并且支持撤销操作

各个供应商提供的on off 都有统一的接口

1. 命令对象中有一个通用的方法: execute()

2. 命令对象（系统中有多个）的所有客户（remote）把每个命令对象看作是一个blackbox。当客户需要请求对象的服务时，只要简单地调用对象的虚拟execute() 方法

