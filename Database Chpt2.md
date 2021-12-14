### 第2章 关系模型介绍
caiyi 2021/5/11

#### 2.1 关系型数据库的结构

**关系**(relation)：表

**元组**(tuple)：行

**属性**(attribute)：列

**域**(domin)：对于关系的每个属性，都存在一个允许取值的集合

关系的所有属性的域都是原子的，被看作是不可再分的单元

**关系模式**(relation schema)：对于关系结构的抽象描述，由属性序列和各属性对应域组成

**关系实例**(relation instance)：一个关系的特定实例



#### 2.2 码

一个关系中没有两个元组在所有属性值上都相等

**超码**(super key)：一个或多个属性的集合，可以唯一标识一个元组

**候选码**(candidate key) ：最小超码，不包括无关紧要的属性

**主码**(primary key)：用来在一个关系中区分不同元组的候选码

**外码**(primay key)：一个关系模式r1可能在它的属性中包括另一个关系模式r2的主码，r1称为外码依赖的参照关系，r2称为外码依赖的被参照关系

**参照性关系**(referential integrity constraint)：要求在参照关系中任意元组在特定属性上的取值必然等于被参照关系中某个元素在特定属性上的取值



#### 2.3 模式图

每个关系用矩形表示，关系名字显示在矩形上方，矩形内列出各种属性

主码属性用下划线标注，外码依赖用从参照关系的外码属性到被参照关系的主码属性之间的箭头来表示

![IMG_6115](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6115.PNG)

#### 2.4 关系查询语言

过程化语言：用户指导系统对数据库执行一系列操作以计算出结果，例如关系代数

非过程化语言：只需描述信息不用给出获取信息的具体方法，例如关系演算TRC、域关系演算DRC

#### 2.5 关系运算

##### **基本操作**

- **选择(select)** $\sigma$

  查询满足给定条件的元组（从行的角度）

  ![image-20210609203247041](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609203247041.png)

- **投影(project)**  $\Pi$

  选出若干属性列组成新的关系（从列的角度）

  投影之后会取消重复的行

  ![image-20210609203309795](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609203309795.png)

- **并(union)**  $\cup$

  先并再去重

  ![image-20210609202449131](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609202449131.png)

- **交(set intersection)** $\cap$

  两个表都有的元组

  ![image-20210609202504184](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609202504184.png)

- **差(set difference)**   $-$

  R有但S没有的关系元组

  ![image-20210609202529031](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609202529031.png)

- **笛卡尔积(Cartesian product)**  $×$

  ![image-20210609202543677](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609202543677.png)

- **自然连接(natural join)**  $\bowtie$

  从两个关系的笛卡尔积中，基于两个关系模式中都出现的属性上的相等性进行选择，最后去掉重复的列

  ![image-20210609202851972](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609202851972.png)

- **除(division)**  $÷$

  保留R中满足S的，而且R中列要去掉S的列

  ![image-20210609202907933](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609202907933.png)

- **改名(rename)**  $\rho$

  $\rho _{x(A1,A2,...An)}(E)$

  返回表达式E的结果，并赋给它名字x，同时将各属性更名为A1,A2,...An

  例子：找出大学里的最高工资

  ![image-20210609203335581](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609203335581.png)

- **赋值(assignment)** $←$

  ![image-20210609203415119](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609203415119.png)

  对于关系代数查询而言，赋值必须是赋给一个临时关系变量，对永久关系的赋值形成了对数据库的修改。

  注意：赋值运算不能增强关系代数的表达能力，但是可以使复杂查询的表达变得简单

  

##### 扩展的关系运算

- **广义投影**  (Generalized Projection)

  ![image-20210609203741577](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609203741577.png)

- **聚集**  (Aggregate Functions)   $\mathcal{G}$

  ![image-20210609203652275](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609203652275.png)

  

  

- **内连接/外连接**

  内连接(Inner Join)：两个关系做自然连接时，连接的结果时满足条件的元组保留下来，不满足条件的元组被舍弃了

  ![image-20210609202925573](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609202925573.png)

  外连接(Outer Join)：如果把舍弃的元组也保留再结果关系中，而在其他属性上填null，叫做外连接

  ![image-20210609202947149](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609202947149.png)

  外连接分为左外连接和右外连接

  ![image-20210609203004612](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609203004612.png)

  ![image-20210609203018908](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609203018908.png)



#### 2.6 课堂例题

![IMG_6097 - 副本](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6097%20-%20%E5%89%AF%E6%9C%AC.PNG)

![image-20210609203811287](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609203811287.png)

![IMG_6097](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6097.PNG)

![image-20210609203820939](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609203820939.png)