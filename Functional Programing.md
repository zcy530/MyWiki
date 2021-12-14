basic inctive logic relation list inp会有



各位同学好，我是张彩仪，大家可以叫我Nicole，现在在华东师范大学读大三，专业是软件工程，我很喜欢微软的企业氛围，性格开朗，喜欢交朋友，希望和大家一起在微软相遇，共同成长，我是一个浪漫和严谨并存的人



推行官

1. 组织微信交流群，活跃气氛
2. 按照学校进行拉群
3. 回答同学问题，申请流程，面试挑战
4. ![image-20211213172414410](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20211213172414410.png)



5. 线下活动 打卡微软食堂
6. 组织和就业办和老师之间的联系
7. 内推 毕业时间2022.9-2023.8 专业match

奖励：

![image-20211213173220684](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20211213173220684.png)

![image-20211213172945554](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211213172950.png)

留意残障人士，如果身边有残障的同学想从事软件开发工作，直接联系hr，一个pwd残障同学是30分

![image-20211213173758382](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211213173802.png)

![image-20211213174115633](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20211213174115633.png)

![image-20211213174942383](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211213174944.png)



![image-20211213180434579](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211213180436.png)

提前批在免笔试这块是一样的，但推面试时会优先考虑这部分同学

![image-20211213180655118](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211213180656.png)

# 一、basic

## 1.1 数据与函数

### 枚举类型

Inductive 定义一个数据集合

```
Inductive day : Type :=
  | monday
  | tuesday
  | wednesday
  | thursday
  | friday
  | saturday
  | sunday.
```

Definition 可以写一些操作函数

```
Definition next_weekday (d:day) : day :=
  match d with
  | monday ⇒ tuesday
  | tuesday ⇒ wednesday
  | wednesday ⇒ thursday
  | thursday ⇒ friday
  | friday ⇒ monday
  | saturday ⇒ monday
  | sunday ⇒ monday
  end.
```

在 Coq 中检验的方式一共有三种：

第一，用 Compute 指令来计算包含 next_weekday 的复合表达式

```
Compute (next_weekday friday).
Compute (next_weekday (next_weekday saturday)).
```

第二，将期望的结果写成 Coq 的示例

```
Example test_next_weekday:
  (next_weekday (next_weekday saturday)) = tuesday.

Proof. simpl. reflexivity.  Qed.
```

这段代码基本上可以读作“若等式两边的求值结果相同，该断言即可得证”

第三，我们可以让 Coq 从 Definition 中提取出用其它更加常规的编程语言编写的程序 



### 布尔值

```
Inductive bool : Type :=
  | true
  | false.
```

布尔值的函数可按照同样的方式来定义

```
Definition negb (b:bool) : bool :=
  match b with
  | true ⇒ false
  | false ⇒ true
  end.
```

```
Definition andb (b1:bool) (b2:bool) : bool :=
  match b1 with
  | true ⇒ b2
  | false ⇒ false
  end.
```

```
Definition orb (b1:bool) (b2:bool) : bool :=
  match b1 with
  | true ⇒ true
  | false ⇒ b2
  end.
```

以下四个单元测试演示了多参数应用的语法

```coq
Example test_orb1: (orb true false) = true.
Proof. simpl. reflexivity. Qed.
Example test_orb2: (orb false false) = false.
Proof. simpl. reflexivity. Qed.
Example test_orb3: (orb false true) = true.
Proof. simpl. reflexivity. Qed.
Example test_orb4: (orb true true) = true.
Proof. simpl. reflexivity. Qed
```

Notation 能为既有的定义赋予新的中缀记法

```
Notation "x && y" := (andb x y).
Notation "x || y" := (orb x y).
Example test_orb5: false || false || true = true.
Proof. simpl. reflexivity. Qed.
```



### 类型

Check 指令会让 Coq 显示一个表达式的类型

```
Check true.
(* ===> true : bool *)
```

像 negb 这样的函数本身也有类型，被称为函数类型，用带箭头的类型表示

```
Check negb
    : bool → bool.
Check andb
    : bool → bool → bool.
```



### 由旧类型构造新类型

我们之前定义的枚举类型，每个元素都只是无参数构造子

下面的类型定义，会让其中一个构造子接受一个参数

```
Inductive rgb : Type :=
  | red
  | green
  | blue.
Inductive color : Type :=
  | black
  | white
  | primary (p : rgb).
```

最后一行表示若 p 是属于 rgb 的构造子表达式，则 primary p（构造子 primary 应用于参数 p）是属于集合 color 的构造子表达式

定义一个关于color的函数

```
Definition monochrome (c : color) : bool :=
  match c with
  | black ⇒ true
  | white ⇒ true
  | primary p ⇒ false
  end.
```

```
Definition isred (c : color) : bool :=
  match c with
  | black ⇒ false
  | white ⇒ false
  | primary red ⇒ true
  | primary _ ⇒ false
  end.
```

 primary _ 是构造子 primary 应用到除 red 之外的任何 rgb 构造子上





### 元组

定义一个由四位字节组成的元组

```
Inductive bit : Type :=
  | B0
  | B1.
  
Inductive nybble : Type :=
  | bits (b0 b1 b2 b3 : bit).
  
Check (bits B1 B0 B1 B0)
    : nybble.
```

```
Definition all_zero (nb : nybble) : bool :=
  match nb with
    | (bits B0 B0 B0 B0) ⇒ true
    | (bits _ _ _ _) ⇒ false
  end.
```



### 数值

我们把这个部分放在一个模块中，这样我们自己对自然数的定义就不会干扰标准库中的自然数

```
Module NatPlayground.
```

大写字母O表示零，当S构造函数应用于自然数n的表示时，结果是n+1，其中S代表后继（successor），可被放在一个自然数之前产生另一个自然数

```
Inductive nat : Type :=
  | O
  | S (n : nat).
```

0 → O，1 → S O，2 → S(S O)，3 → S(S(S O))，以此类推

定义自然数的前趋函数

```
Definition pred (n : nat) : nat :=
  match n with
    | O ⇒ O
    | S n' ⇒ n'
  end.
```

定义自然数减法函数

```
Definition minustwo (n : nat) : nat :=
  match n with
    | O ⇒ O
    | S O ⇒ O
    | S (S n') ⇒ n'
  end.
Compute (minustwo 4).
(* ===> 2 : nat *)
```

```
End NatPlayground.
```

Coq 会默认将自然数打印为十进制形式

```
Check (S (S (S (S O)))).
(* ===> 4 : nat *)
```



### 递归

关键字 Fixpoint 可用于定义递归函数

比如判断自然数是否为偶数

```
Fixpoint evenb (n:nat) : bool :=
  match n with
  | O ⇒ true
  | S O ⇒ false
  | S (S n') ⇒ evenb n'
  end.
```

判断自然数是否为奇数

```
Definition oddb (n:nat) : bool :=
  negb (evenb n).
```

```
Example test_oddb1: oddb 1 = true.
Proof. simpl. reflexivity. Qed.
Example test_oddb2: oddb 4 = false.
Proof. simpl. reflexivity. Qed.
```

递归多参数函数

```
Module NatPlayground2.

Fixpoint plus (n : nat) (m : nat) : nat :=
  match n with
    | O ⇒ m
    | S n' ⇒ S (plus n' m)
  end
```

便于理解以上函数可以看看这个化简步骤

```
(*   plus 3 2
i.e. plus (S (S (S O))) (S (S O))
 ==> S (plus (S (S O)) (S (S O)))
      （根据第二个 match 从句）
 ==> S (S (plus (S O) (S (S O))))
      （根据第二个 match 从句）
 ==> S (S (S (plus O (S (S O)))))
      （根据第二个 match 从句）
 ==> S (S (S (S (S O))))
      （根据第一个 match 从句）
i.e. 5  *)
```

两个自然数的乘法

```
Fixpoint mult (n m : nat) : nat :=
  match n with
    | O ⇒ O
    | S n' ⇒ plus m (mult n' m)
  end.
Example test_mult1: (mult 3 3) = 9.
Proof. simpl. reflexivity. Qed.
```

两个自然数相减

```
Fixpoint minus (n m:nat) : nat :=
  match n, m with
  | O , _ ⇒ O
  | S _ , O ⇒ n
  | S n', S m' ⇒ minus n' m'
  end.
  
End NatPlayground2.
```

自然数的幂

```
Fixpoint exp (base power : nat) : nat :=
  match power with
    | O ⇒ S O
    | S p ⇒ mult base (exp base p)
  end.
```

比较两个自然数是否相等

```
Fixpoint eqb (n m : nat) : bool :=
  match n with
  | O ⇒ match m with
         | O ⇒ true
         | S m' ⇒ false
         end
  | S n' ⇒ match m with
            | O ⇒ false
            | S m' ⇒ eqb n' m'
            end
  end.
```

第一个参数是否小于等于第二个参数

```
Fixpoint leb (n m : nat) : bool :=
  match n with
  | O ⇒ true
  | S n' ⇒
      match m with
      | O ⇒ false
      | S m' ⇒ leb n' m'
      end
  end.
```

第一个参数是否严格小于第二个参数

```
Definition ltb (n m:nat) : bool :=
  (negb(eqb n m)) && (leb n m)
```

为了方便我们引入notation来记这几个常用的函数

```
Notation "x + y" := (plus x y)
                       (at level 50, left associativity)
                       : nat_scope.
Notation "x - y" := (minus x y)
                       (at level 50, left associativity)
                       : nat_scope.
Notation "x * y" := (mult x y)
                       (at level 40, left associativity)
                       : nat_scope.
Notation "x =? y" := (eqb x y) (at level 70) : nat_scope.
Notation "x <=? y" := (leb x y) (at level 70) : nat_scope.
```



## 1.2 基于化简的证明

**simpl** 化简等式两边

**reflexivity** 检查两边是否具有相同的值，会自动做一些化简

**intros** n 假设存在一个任意自然数 n，将量词从证明目标转移到当前假设的上下文中

**Example** 和 **Theorem** 表示完全一样的东西

**策略**是一条可以用在 Proof 和 Qed（证毕）之间的指令，告诉 Coq 如何来检验我们所下的断言的正确性

例如：

```
Theorem plus_O_n : forall n : nat, 0 + n = n.
Proof.
  intros n. reflexivity.  Qed.
```

```
Theorem plus_1_l : forall n:nat, 1 + n = S n.
Proof.
  intros n. reflexivity. Qed.
```

```
Theorem mult_0_l : forall n:nat, 0 × n = 0.
Proof.
  intros n. reflexivity. Qed.
```

后缀 _l 读作“在左边”



## 1.3 基于改写的证明

**intros** 将前提从证明目标移到当前上下文的假设中

**rewrite** 用来告诉 Coq 执行这种替换的策略

**Admitted** 指令告诉 Coq 我们想要跳过此定理的证明

例子一：

```
Theorem plus_id_example : ∀ n m:nat,
  n = m →
  n + n = m + m.
```

该定理并未对自然数 n 和 m 所有可能的值做全称断言，而是讨论了仅当 n = m 时这一更加特定情况

```
Proof.
  (* 将两个量词移到上下文中： *)
  intros n m.
  (* 将前提移到上下文中： *)
  intros H.
  (* 用前提改写目标： *)
  rewrite → H.
  reflexivity. Qed.
```

第一行将全称量词变量 n 和 m 移到上下文中

第二行将前提 n = m 移到上下文中，并将其命名为 H

第三行告诉 Coq 改写当前目标（n + n = m + m），把前提等式 H 的左边替换成右边



例子二：

```
Theorem plus_id_exercise : ∀ n m o : nat,
  n = m → m = o → n + m = m + o.
Proof.
  intros n m o. intros H1 H2.
  rewrite H1. rewrite H2. reflexivity.
Qed.
```



**Check** 命令也可用来检查以前声明的引理和定理

```
Check mult_n_O.
(* ===> forall n : nat, 0 = n * 0  *)
Check mult_n_Sm.
(* ===> forall n m : nat, n * m + n = n * S m  *)
```

除了上下文中现有的假设外，还可以通过 rewrite 策略来运用前期证明过的定理

```
Theorem mult_n_0_m_0 : ∀ n m : nat,
  (n × 0) + (m × 0) = 0.
Proof.
  intros n m.
  rewrite <- mult_n_O.
  rewrite <- mult_n_O.
  reflexivity. Qed.
```

```
Theorem mult_n_1 : ∀ n : nat,
  n × 1 = n.
Proof.
  intros.
  rewrite <- mult_n_Sm.
  rewrite <- mult_n_O.
  reflexivity. Qed.
```



## 1.4 利用情况分析来证明

**destruct** 分别对 n = 0 和 n = S n' 这两种情况进行分析的策略

### 例一

```
Theorem plus_1_neq_0 : ∀ n : nat,
  (n + 1) =? 0 = false.
Proof.
  intros n. destruct n as [| n'] eqn:E.
  - reflexivity.
  - reflexivity. Qed.
```

**destruct** 生成两个子目标，然后我们分别证明

**as [| n']** 是介绍模式，指出变量，变量之间用|分开。第一个组件是空的，因为O的构造函数是空的，第二个组件n'，因为S是一元构造函数

**eqn:E** 注释告诉析构函数给这个方程命名E

**— 符号** 标明这两个生成的子目标所对应的证明部分



### 例二

证明布尔值的取反是对合（Involutive）的 

```
Theorem negb_involutive : ∀ b : bool,
  negb (negb b) = b.
Proof.
  intros b. destruct b eqn:E.
  - reflexivity.
  - reflexivity. Qed.
```

destruct 没有 as 子句，因为此处 destruct 生成的子分类均无需绑定任何变量



### 例三

在一个子目标内调用 destruct，产生出更多的证明义务，使用不同的标号来标记目标的不同层级

```
Theorem andb_commutative : ∀ b c, andb b c = andb c b.
Proof.
  intros b c. destruct b eqn:Eb.
  - destruct c eqn:Ec.
    + reflexivity.
    + reflexivity.
  - destruct c eqn:Ec.
    + reflexivity.
    + reflexivity.
Qed.
```



### 例四

除了 - 和 + 之外，还可以使用 ×  -- ***，也可以用花括号将每个子证明目标括起来

```
Theorem andb_commutative' : ∀ b c, andb b c = andb c b.
Proof.
  intros b c. destruct b eqn:Eb.
  { destruct c eqn:Ec.
    { reflexivity. }
    { reflexivity. } }
  { destruct c eqn:Ec.
    { reflexivity. }
    { reflexivity. } }
Qed.
```

花括号还允许我们在一个证明中的多个层级下使用同一个标号

```
Theorem andb3_exchange :
  ∀ b c d, andb (andb b c) d = andb (andb b d) c.
Proof.
  intros b c d. destruct b eqn:Eb.
  - destruct c eqn:Ec.
    { destruct d eqn:Ed.
      - reflexivity.
      - reflexivity. }
    { destruct d eqn:Ed.
      - reflexivity.
      - reflexivity. }
  - destruct c eqn:Ec.
    { destruct d eqn:Ed.
      - reflexivity.
      - reflexivity. }
    { destruct d eqn:Ed.
      - reflexivity.
      - reflexivity. }
Qed.
```

最后说一种简便写法，很多证明在引入变量之后会立即对它进行情况分析：

```
intros x y. destruct y as [|y] eqn:E.
```

但可以通过使用介绍模式而不是变量名来对变量进行案例分析

```
Theorem plus_1_neq_0' : ∀ n : nat,
  (n + 1) =? 0 = false.
Proof.
  intros [|n].
  - reflexivity.
  - reflexivity. Qed.
```

如果没有需要命名的构造子参数，只需写上 [] 即可进行情况分析

```
Theorem andb_commutative'' :
  forall b c, andb b c = andb c b.
Proof.
  intros [] [].
  - reflexivity.
  - reflexivity.
  - reflexivity.
  - reflexivity.
Qed.
```



#### 练习：

```
Theorem zero_nbeq_plus_1 : forall n : nat,
  0 =? (n + 1) = false.
Proof.
  intros [| n'].
  -simpl. reflexivity.
  -simpl. reflexivity.
Qed.
```

```
Theorem andb_true_elim2 : forall b c : bool,
  andb b c = true -> c = true.
Proof.
  intros b c. destruct c.
  - reflexivity.
  - destruct b.
    + intros. rewrite <- H. reflexivity.
    + intros. rewrite <- H. reflexivity.
Qed.
```



## 1.5 更多练习

证明以下关于布尔函数的定理

```
Theorem identity_fn_applied_twice :
  ∀ (f : bool → bool),
  (∀ (x : bool), f x = x) →
  ∀ (b : bool), f (f b) = b.
Proof.
  (* 请在此处解答 *) Admitted.
```

