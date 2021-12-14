## 第8章 关系数据库设计

### 8.1 为什么要引入范式

1. 数据冗余

   比如姓名重复出现浪费空间

2. 更新异常

   更新后造成数据不一致，比如班主任换名字，每个学生对应的每行都得换

3. 插入异常

   应该插入的无法被插入

4. 删除异常

   不该删除的被删除了

所以我们引入一个规范的方法判断一个关系模式是否应该分解

### 8.2 概念

#### 8.2.1 符号表示法

用希腊字符 $\alpha$、$\beta$ 等表示属性集，用小写罗马字母后括住大写字母 $r(R)$ 指关系模式

当属性集是一个超码时用K表示，超码属于特殊的关系模式

#### 8.2.2 码的概念

**超码** (super key)：能推出所有属性的属性集，唯一能够标识整条元组的属性集。R的子集K是 r(R) 的超码的条件是：在关系 r(R) 的任意合法实例中，对于r的实例中的所有元组对t1和t2总满足，若t1 != t2，则t1[K] != t2[K]

**候选码**：可以推出所有的属性，但是他的任意一个真子集无法退出所有的属性，候选码是最小的超码

**主码**：从候选码中任意挑一个作为主码

**主属性**：包含在任意一个候选码中的属性，如下题的ABCDE

**非主属性**：不包含在任意一个候选码中的属性，如下题的G

**码**：把主码、候选码简称为码

**全码**：如果所有属性都是码，成为全码



**求候选码的步骤**：

step1：只出现在左边的一定是候选码

step2：只出现在右边的一定不是候选码

step3：左右都出现的不一定

step4：左右都不出现的一定是候选码

step5：求确定的候选码的闭包（closure，指由他可以推出来的所有属性），如果可以推出全部，那么当前确定的就是候选码。否则就把每个可能的码，放进当前确定的候选码里面进行求闭包

例题：![IMG_6121](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6121.PNG)

####8.2.3 函数依赖 (function dependency)

![image-20210609212220049](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609212220049.png)

3. **最小函数依赖集**：即F中的每个依赖，都不可以被其他依赖推出

   step1：把右边的元素拆分成单个的

   step2：除去当前元素，求它的闭包，把集合里面所有元素一一排查

   step3：左边最小化（通过遮住元素来看能不能推出其他元素），比如BCD，遮住B看能不能推出B，再遮住C/D

![IMG_6123](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6123.PNG)

### 8.3 范式

**1NF**：原子性，不可分割

**2NF**：不存在<u>非主属性</u>对码的<u>部分函数依赖</u> 

**3NF**：不存在<u>非主属性</u>对码的<u>传递函数依赖</u>，全码一定是3NF

**BCNF**：<u>主属性和非主属性</u>都不存在对码的<u>部分函数依赖和传递函数依赖</u>

**4NF**：关系模式R属于第三范式，且消除了非主属性对候选键以外属性的多值依赖。

BCNF 消除了所有基于函数依赖能够发现的冗余，具有函数依赖集F的关系模式R属于BCNF的条件是，对F+中所有形如 $\alpha \rightarrow \beta$ 的函数依赖下面至少有一项成立：$\alpha \rightarrow \beta$ 是平凡的函数依赖，或 $\alpha$ 是模式 R 的一个超码 

**范式判断：**

1. 求候选键，和主属性/非主属性

2. 非键属性是否**部分依赖**于候选键

   部份依赖是指如果候选码是AB非键C，如果在F中找到A→C或者B→C，就是部分依赖

   如果是：1NF

   如果否：往下走

3. 非键属性是否**传递依赖**于候选键

   如果是：2NF

   如果否：往下走

4. 所有依赖项的左边是否全为候选键

   如果是：BCNF

   如果不是：3NF

   

### 8.4 函数依赖理论

####8.4.1 函数依赖集的闭包

**逻辑蕴含**(logically imply)：如果函数依赖集 F 能推出函数依赖 f ，则称 f 被 F 逻辑蕴含。

**函数依赖集的闭包**(closure)：令F为一个函数依赖集，F的闭包是被F逻辑蕴含的所有函数依赖的集合，记作F+



####8.4.2 Armstrong公理

![image-20210609212335949](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609212335949.png)

####8.4.3 属性集的闭包  (Attribute Closure)

![image-20210609212352748](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609212352748.png)

####8.4.4 正则覆盖 (Cononical Coverage)

![image-20210609212409022](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609212409022.png)

####8.4.5 无损分解(lossless decompositon)

![image-20210609212426101](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210609212426101.png)

**判断无损分解**：

当且仅当只被分解为两个关系时：

![IMG_6139](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6139.PNG)

当分解为多个关系时：

![IMG_6124](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6124.PNG)

![IMG_6125](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6125.PNG)

####8.4.6 保持依赖

判断是否保持依赖：对于关系模式R(U,F)，设R1(U1, F1), R2(U1,F2), ... Rn(Un, Fn)是R的分解，若F的闭包等于$F1\cup F2\cup ...\cup Fn$ 的闭包，则称该分解是保持函数依赖

![IMG_6126](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6126.PNG)

### 8.5 范式分解算法

**模式分解的要求：**

1. 无损连接性：具有无损连接性的分解不一定能够保持函数依赖
2. 保持函数依赖：保持函数依赖的分解不一定具有无损连接性

**模式分解步骤**：

1. **求候选码**

2. **求3NF分解**

   - 求最小函数依赖集

   - 把最小函数依赖集箭头前后的元素写在一起作为一个Ri

3. **求BCNF分解**

   - INPUT 关系模式R以及函数依赖集F，初始化 P={R}

   - 若P中的所有关系模式S都是BCNF，则转步骤（4）
   - 若P中有一个模式S不是BCNF，则S中必能找到一个函数依赖X→Y，X不是S的候选码，且Y不属于X（根据BCNF的定义）
   - 设S1 = XY，S2 = S-Y，分解后的{S1, S2}代替S，转步骤（2）
   - END

![IMG_6133](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6133.PNG)

![IMG_6132](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6132.PNG)