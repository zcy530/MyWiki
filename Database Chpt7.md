### 第7章 数据库设计和E-R模型
2021/5/11
#### 7.1 设计步骤

需求分析

概念结构设计   ER图或者是设计数据字典

逻辑结构设计   把ER图转为逻辑模型

物理结构设计   把逻辑模型转为物理模型

数据库实施       写SQL代码

#### 7.2 实体-联系模型

E-R模型的三个要素：实体集、联系集、属性

1. **实体**(entity)：在现实世界中存在并且区别于其他对象的事物或对象，

   **实体集**(entity set)：相同类型即具有相同性质的实体集合，例如大学所有教师的集合instructor

2. **联系**(relationship)：指多个实体间相互关联

   **联系集**(relationship set)：相同类型联系的集合

   **多元联系集**：相同的实体集可能会参与到多个联系集中

![IMG_6107](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6107.PNG)

3. **实体属性**：实体集中每个成员所拥有的描述性性质

   **描述性属性**：例如考虑instructor和student之间的联系集advisor，可以将属性date与该联系关联

![IMG_6102](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6102.PNG)

     E-R模型中的属性可以按照如下的属性类型来进行划分：
    
     **简单/复合属性**(simple/composite)：简单属性不能划分为更小的部分
    
     **单值/多值属性**(single/multivalued)：一个学生只能有一个student_id，但可以有多个tele_number
    
     **派生属性**(derived)：这类属性的值可以从别的相关属性或实体派生出来

![IMG_6103](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6103.PNG)

4. **映射基数**(mapping cardinality)：表示一个实体通过联系集可以相关联的实体的个数

   one-to-one：就任总统（总统，国家）

   one-to-many：分班情况（班级，学生）

   many-to-one：就医（病人，医生）

   many-to-many：选课（学生，课程）




5. **参与约束**

   全部参与：实体集E中的每个实体都参与到联系集R的至少一个联系中

   部分参与：实体集E中只有部分实体参与到R的联系中

   例如：在图7.5(a)中，B在联系集是全部参与，A是部分参与

   例如：每个student都要联系至少一个instructor，但是一个instructor不是一定要指导一个学生

6. **联系集的主码结构依赖于联系集的映射函数：**

   以instructor和student的联系集advisor举例

   one-to-one：由instructor和student两个候选码中的任意一个作为主码

   one-to-many：advisor的主码是student的主码

   many-to-one：advisor的主码是instructor的主码

   many-to-many：advisor的主码由instructor和student的并集组成
   ![IMG_6106](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6104.PNG)
   ![IMG_6106](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6105.PNG)

#### 7.3 E-R图构建

1. **基本结构**

   菱形：联系集

   矩形：集的属性

   线段：将实体集连接到联系集

   虚线：将联系集属性连接到联系集

   双线：显示实体在联系集中的参与度

   双菱形：代表连接到弱实体集的标志性联系集

2. **映射基数**

   用双线表示

   用箭头表示

   ![IMG_6106](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6106.PNG)

   用线段上的l...h标注，l表示最小的映射基数，h表示最大的映射基数

   ![IMG_6107](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6107.PNG)

3. **复杂的属性**

   复合属性有name，address，street

   其中street的子属性包括street_number, street_name, apt_number

   多重属性有{phone_number}

   派生属性age()

   ![IMG_6108](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6108.PNG)

4. **角色**

   实体的角色有时不止有一个

   在菱形和矩形间的连线上进行标注表示角色

   ![IMG_6109](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6109.PNG)

5. **弱实体集**

   **弱实体集**(week entity set)：实体集的所有属性都不足以形成主码

   **强实体集**(strong entity set)：具有主码的实体集

   **标识性联系**(identifying)：弱实体集必须与另一个称作**标识**或**属主实体集**的实体集关联才能有意义

   注意：强实体与弱实体的标识性联系联系只能是1：1或1：N，弱实体参与联系时应该是**全部参与**

   **分辨符**(discriminator)：区分弱实体集中的实体的方法

   弱实体集的主码由标识实体集的主码加上该弱实体集的分辨符构成

   

   弱实体集在E-R图中的表示：

   		分辨符号用<u>虚线下划线</u>标明，而不是实线
   	
   		关联强弱实体集的联系集用<u>双菱形</u>表示
   	
   		弱实体与联系集之间画成<u>双线边</u>，联系集画<u>指向强实体集的箭头</u>

   ![IMG_6110(20210508-133852)](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6110(20210508-133852).PNG)


6. **大学中的E-R图举例**

![IMG_6111(20210508-175125)](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6111(20210508-175125).PNG)

#### 7.4 E-R图转化为关系模型

1. **具有简单属性的强实体集的表示**

   指一对多中的多的实体集，强实体集的主码就是生成的模式的主码

   比如：图7-15   student( <u>ID</u>, name, tot_cred )

2. **具有复杂属性的强实体集的表示**

   如果是复合属性，将该属性用它的子属性们替代了

   例如：图7-11   instructor( ID, first_name, middle_initial, last_name, street_number, street_name,apt_number, city, state, zip_code, date_of_birth )

   如果是多值属性，新构建一个关系，包含这个多值属性，和它对应所在的实体集或联系集的主码

   例如：图7-11   instructor_phone( <u>ID</u>, <u>phone_number</u> )

3. **弱实体集的表示**

   主码由所依赖的强实体集的主码和弱实体集的分辨符组成

   例如：图7-15   section( <u>course_id</u>, <u>sec_id</u>, <u>semester</u>, <u>year</u> )

   级联删除：如果一个course实体被删除，那么所有与它相关联的section实体也被删除

4. **联系集的表示**

   **多对多**的二元联系：该联系集属性自成一个关系，主码是参与实体集的主码的并集

   **一对多**的二元联系：联系集的属性归到多的一方，少的一方的主码也要加到多的一方

   **一对一**的二元联系：联系集的属性归到任意一方，另一方的主码也要加进去

   边上没有箭头的N元联系集：主码是所有实体集主码的并集

   边上有一个箭头的N元联系集：主码为不在箭头侧的实体集的主码

   ![IMG_6112](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6112.PNG)

   **模式的冗余**

   一般连接弱实体集与其所依赖的强实体集的联系集的模式是冗余的，在E-R图中省略

   **模式的合并**

   多对一的联系集的和多的那一方可以合并，主码是多的那一方的主码，少的一方的主码也要加到多的一方

   ![IMG_6116](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6116.PNG)

#### 7.5 E-R设计问题

一个对象不能同时作为实体和属性

一个实体集不能与另一个实体集的属性相关联，只能实体与实体相关联

#### 7.6 扩展的E-R属性

1. **特化**(specialization)：在实体集内部进行分组的过程

   每个特化的实体都包括实体集的所有属性以及附加属性

   一个实体集可以根据多个可区分的特征进行特化，某个特定实体集可能同时属于多个特化集

   在E-R图中，特化用从特化实体指向另一方的空心箭头表示，成为**ISA关系**

   **重叠特化**(overlapping specialization)：一个实体属于多个特化实体集，分开使用<u>两个箭头</u>

   **不相交特化**(disjoin specialization)：至多属于一个特化实体集，使用<u>一个箭头</u>

   

2. **概化**(generalization)：高层实体集与一个或多个底层实体集间的包含关系

   高层与低层实体集可以分别称作**超类**(superclass)和**子类**(subclass)

   在E-R图中对概化和特化的表示不作区分，区别在于出发点和总体目标

   **特化**从单一的实体集出发，通过创建不同的低层实体集，来<u>强调同一实体集中不同实体间的差异性</u>

   **概化**是在这些实体集的共性的基础上，将它们综合成一个高层实体集，<u>强调相似性</u>

   ![IMG_6117](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6117.PNG)

3. **属性继承**(attribute inheritance)

   低层实体集继承高层实体集的属性

   低层实体集继承高层实体集所参与的联系集

4. **聚集**(agrregation)：是一种抽象，将联系视为高级实体

   例如：我们将联系集 proj_guide(instructor, student, project) 看成一个高级实体集，可以像对任何其他实体集一样来处理，就可以在proj_guide和evaluation之间创建一个二元联系eval_for

   ![IMG_6119](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6119.PNG)

5. **概化上的约束**

   **不相交**(disjoint)：一个实体至多属于一个低层实体集

   **重叠**(overlapping)：同一个实体可以同时属于一个概化中的多个低层实体集，比如某些雇员可以参加到多个工作组当中，因此是重叠的

   **全部概化**(total generalization)：每个高层实体必须属于一个低层实体集

   **部分概化**(partial generalization)：允许一些高层实体不属于任何低层实体集

   ![IMG_6120(20210509-153942)](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/IMG_6120(20210509-153942).PNG)

6. **转化为关系模式**

   **概化的表示**

   为高层实体集创建一个模式，为每个低层实体集创建一个模式

   person( <u>ID</u>, name, street, city )

   employee( <u>ID</u>, salary )

   student( <u>ID</u>, tot_cred )

   如果概化是不相交且完全的，即如果不存在同时属于两个同级的低层实体集的实体，且如果高层实体集的任何实体也都是某个低层实体集的成员，可以不需要为高层实体集创建模式

   employee( <u>ID</u>, name, street, city, salary )

   student( <u>ID</u>, name, street, city, tot_cred )

   **聚集的表示**