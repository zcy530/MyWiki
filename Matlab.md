# Matlab

zcy

## 第二章

### 2.1 数据类型

matlab中有15种基本数据类型，每种数据类型均以数组/矩阵的形式出现

**整数**

matlab支持1、2、4、8字节的有符号整数和无符号整数

![image-20210929220230781](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210929220237.png)

**浮点数**

有单精度和双精度两种浮点数

![image-20210929221858672](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210929221906.png)

**复数**

复数包含实部和虚部，可以用i或者j来表示虚部



### 2.2 基本矩阵操作

#### 2.2.1 矩阵的构造

#### 2.2.2 矩阵大小的改变

#### 2.2.3矩阵下标引用

### 2.3 运算符和特殊符号

### 2.4 字符串处理函数

## 第三章 数学运算

### 3.1 矩阵运算

#### 3.1.1 矩阵分析

![image-20210928204148903](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210928204300.png)

- **向量间的距离 norm()**

  计算和原点的距离：N = norm(E,2)

  ```matlab
  >> norm([1:5],2)
  
  ans =
  
       7.4162
  ```

  计算两个向量间的距离：N = norm(E)

  ```matlab
  >> x = [1,2,3,4,5];
  >> y = [3,0,5,2,2];
  >> e = x-y;
  >> norm(e)
  
  ans =
  
       5
  ```

  

- **矩阵的秩 rank()**

  矩阵中线性无关的列向量个数成为列秩，线性无关的行向量个数成为行秩

  ```matlab
  >> eye(4)
  
  ans =
  
       1     0     0     0
       0     1     0     0
       0     0     1     0
       0     0     0     1
  
  >> rank(eye(4))
  
  ans =
  
       4
  ```

  

- **矩阵的行列式 det()**

  ![image-20210928214852299](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210928214854.png)

  ```matlab
  >> A = [1 2 3;4 5 6;7 8 9];
  >> A_det = det(A)
  
  A_det =
  
         0
  ```

  行列阵为0的矩阵为奇异矩阵，用函数 cond() 进行判定

  

- **矩阵的迹 trace()**

  矩阵对角元素之和

  ```matlab
  >> disp(['trace of A = ',num2str(trace(A))]);
  trace of A = 15
  >> A = [1 2 3;4 5 6;7 8 9];
  >> disp(['trace of A = ',num2str(trace(A))]);
  trace of A = 15
  ```

  

- **矩阵的化零矩阵  null()**

  对于非满秩矩阵A，若存在矩阵Z使得 AZ = 0 且 Z的转置Z = I，则称矩阵Z 为矩阵A的化零矩阵

  ```matlab
  >> A = [1 2 3;1 2 3;4 5 6];
  >> Z = null(A)
  
  Z =
  
     -0.4082
      0.8165
     -0.4082
   
  >> A*Z
  
  ans =
  
     1.0e-14 *
  
           0
           0
     -0.1776
  
  >> Z'*Z
  
  ans =
  
      1.0000
  ```

  

- **矩阵的正交空间 orth()**

  矩阵A的正交空间Ｑ满足Q*Q’=I, 且Ｑ与Ａ具有共同的列基底

  ```matlab
  >> A = [1 2 3;4 5 6;7 8 9;10 11 12];
  >> Q = orth(A)
  
  Q =
  
     -0.1409    0.8247
     -0.3439    0.4263
     -0.5470    0.0278
     -0.7501   -0.3706
  
  >> Q'*Q
  
  ans =
  
      1.0000   -0.0000
     -0.0000    1.0000
  ```

  

- **矩阵的简化梯形形式  rref()**

  ![image-20210928221508173](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210928221509.png)

  ```matlab
  >> A = [1 2 3 4;1 1 5 6;1 2 3 6;1 1 5 7];
  >> rref(A)
  
  ans =
  
       1     0     7     0
       0     1    -2     0
       0     0     0     1
       0     0     0     0
  ```

  

- **矩阵空间之间的角度 subspace()**

  矩阵空间之间的角度代表具有相同行数的两个矩阵的线性相关程度.夹角越小代表线性相关程度越高

  ```matlab
  >> A = [1 2 3;4 5 6;7 8 9];
  >> B = [1 2;3 4;5 6];
  >> subspace(A,B)
  
  ans =
  
     9.2918e-16
  ```

  

#### 3.1.2 线性方程组

求线性方程组 AX = B 的解

A\B 相当于 inv(A) * B，其中 inv(A) 是矩阵A的逆

```matlab
>> A = magic(3)

A =

     8     1     6
     3     5     7
     4     9     2

>> B = [1;2;3];
>> A\B

ans =

    0.0500
    0.3000
    0.0500
```

用matlab求解以下方程
$$
\left\{
	\begin{array}{c}
		x+2y+3z=5\\
		2x+4y+6z=2\\
		x+3y+7z=12
	\end{array}
\right.
$$

```matlab
>> A = [1 2 3;2 4 6;1 3 7];
>> B = [5;2;12];
>> pinv(A)*B

ans =

   -2.6714
   -2.5429
    3.1857

>> inv(A)*B
警告: 矩阵为奇异工作精度。 
 
>> A\B
警告: 矩阵为奇异工作精度。
```

注意：如果矩阵不是方阵，或是奇异方阵，可以用矩阵的**伪逆pinv(A)** 给出方程组的一个解或最小二乘意义下的最优解，即 **pinv(A)*B**

#### 3.1.3 矩阵分解

矩阵分解是把一个矩阵分解成比较简单或者对它的性质比较熟悉的若干个矩阵的乘积的形式

![image-20210928223743711](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210928223745.png)

- **Cholesky分解** chol()

  **正定矩阵**: 设M是n阶方阵，如果对任何非零向量z，都有 z’Mz > 0，就称M为正定矩阵

  把对称正定矩阵Ａ表示为上三角矩阵R的转置与其本身的乘积，即A=R’R

  ```matlab
  >> a=[4  -1  1; -1  4.25  2.75; 1  2.75  3.5]
  
  a =
  
      4.0000   -1.0000    1.0000
     -1.0000    4.2500    2.7500
      1.0000    2.7500    3.5000
  
  >> chol(a)
  
  ans =
  
      2.0000   -0.5000    0.5000
           0    2.0000    1.5000
           0         0    1.0000
  
  >> A = pascal(4)
  
  A =
  
       1     1     1     1
       1     2     3     4
       1     3     6    10
       1     4    10    20
  
  >> chol(A)
  
  ans =
  
       1     1     1     1
       0     1     2     3
       0     0     1     3
       0     0     0     1
  ```

  

- **LU分解** lu()

  将任意一个方阵A分解为一个<u>置换下三角矩阵L、一个上三角矩阵Ｕ</u>的乘积，即 A = LU

  ```matlab
  >> A = [1 4 2;5 6 9;4 1 8];
  >> [L1,U1] = lu(A)
  
  L1 =
  
      0.2000   -0.7368    1.0000
      1.0000         0         0
      0.8000    1.0000         0
  
  
  U1 =
  
      5.0000    6.0000    9.0000
           0   -3.8000    0.8000
           0         0    0.7895
  ```

  将任意一个方阵A分解为一个<u>下三角矩阵L、一个上三角矩阵Ｕ、置换矩阵P</u>，满足 P * X = L * U

  ```matlab
  >> A = [1 4 2;5 6 9;4 1 8];
  >> [L2,U2,P] = lu(A)
  
  L2 =
  
      1.0000         0         0
      0.8000    1.0000         0
      0.2000   -0.7368    1.0000
  
  
  U2 =
  
      5.0000    6.0000    9.0000
           0   -3.8000    0.8000
           0         0    0.7895
  
  
  P =
  
       0     1     0
       0     0     1
       1     0     0
  ```

  PS：置换矩阵是一种系数只由0和1组成的方块矩阵。置换矩阵的每一行和每一列都恰好有一个1，其余的系数都是0

  

- **QR分解 **qr()

  将mxn的矩阵A分解为<u>mxn的矩阵Ｑ、nxn的上三角矩阵Ｒ</u>的乘积，即A=Q\*R,且Q'\*Q=I

  ```matlab
  >> A = [1 4 2;5 6 9];
  >> [Q,R] = qr(A)
  
  Q =
  
     -0.1961   -0.9806
     -0.9806    0.1961
  
  
  R =
  
     -5.0990   -6.6679   -9.2175
           0   -2.7456   -0.1961
  
  >> qr(A) //返回上三角矩阵R
  
  ans =
  
     -5.0990   -6.6679   -9.2175
      0.8198   -2.7456   -0.1961 //为啥跟上面的R不一样
  ```

  

- **奇异值分解**

  将mxn的矩阵A分解为A=U\*S\*V'，U为mxm的酉方阵，Ｖ为nxn的酉方阵，Ｓ为mxn的酉方阵

  ![image-20210928233557545](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210928233600.png)

  ```matlab
  >> A=[1 4 2;5 6 9];
  >> [U S V]=svd(A)
  
  U =
  
      0.3243    0.9460
      0.9460   -0.3243
  
  
  S =
  
     12.5742         0         0
           0    2.2111         0
  
  
  V =
  
      0.4019   -0.3054   -0.8632
      0.5545    0.8314   -0.0360
      0.7287   -0.4642    0.5035
  ```

  

- **Schur分解 **schur()

  将复方阵A分解为A=U\*L\*U',其中U为酉矩阵，L为上三角矩阵，其对角线元素为A的特征值

  ```matlab
  >> A=[1 4 2;5 6 9;4 1 8];
  [U L]=schur(A)
  
  U =
  
      0.3494    0.8929    0.2838
      0.8242   -0.1489   -0.5464
      0.4456   -0.4248    0.7880
  
  
  L =
  
     12.9859   -0.3899    7.2707
           0   -0.4658   -3.9981
           0         0    2.4799
  ```

  

#### 3.1.4 矩阵的特征值和特征向量

d = eig(A) 返回矩阵A的所有特征值

[V,D] = eig(A) 返回矩阵A的所有特征值和特征向量

```
>> A=[6 12 19;-9 -20 -33;4 9 15]

A =

     6    12    19
    -9   -20   -33
     4     9    15

>> eig(A)

ans =

  -1.0000 + 0.0000i
   1.0000 + 0.0000i
   1.0000 - 0.0000i
```

```
>> X=[-2 1 1;0 2 0;-4 1 3];
>> [V D]=eig(X)

V =

   -0.7071   -0.2425    0.3015
         0         0    0.9045
   -0.7071   -0.9701    0.3015


D =

    -1     0     0
     0     2     0
     0     0     2
```



#### 3.1.5 矩阵的相似变换

对于方阵A和非奇异矩阵B可得到相似矩阵 X = B逆 * A * B

- 对角阵变换
- Jordan变换

#### 3.1.6 非线性运算

![image-20210929214450003](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210929214451.png)



### 3.2 矩阵元素运算

#### 3.2.1 三角函数

![image-20210928204833162](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210928204835.png)

例：计算矩阵每个元素的正弦，以弧度为单位

```matlab
>> A=[6 12 19;-9 -20 -33;4 9 15]

A =

     6    12    19
    -9   -20   -33
     4     9    15

>> Y=sin(A)

Y =

   -0.2794   -0.5366    0.1499
   -0.4121   -0.9129   -0.9999
   -0.7568    0.4121    0.6503
```



#### 3.2.2 指数和对数函数

![image-20210928205609952](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210928205609952.png)

![image-20210928205620086](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210928205622.png)

例，计算矩阵A=[6 12 19;-9 -20 -33;4 9 15]每个元素的指数(e的幂次)

```matlab
>> A=[6 12 19;-9 -20 -33;4 9 15];
>> exp(A)

ans =

   1.0e+08 *

    0.0000    0.0016    1.7848
    0.0000    0.0000    0.0000
    0.0000    0.0001    0.0327
```



#### 3.2.3 复数函数

![image-20210928205653054](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210928205655.png)

例如，计算矩阵A=[6 3+4i -19;5 1-1i 2;-4 0 15]每个元素的模

```matlab
>> A=[6 3+4i -19;5 1-1i 2;-4 0 15]

A =

   6.0000 + 0.0000i   3.0000 + 4.0000i -19.0000 + 0.0000i
   5.0000 + 0.0000i   1.0000 - 1.0000i   2.0000 + 0.0000i
  -4.0000 + 0.0000i   0.0000 + 0.0000i  15.0000 + 0.0000i

>> abs(A)

ans =

    6.0000    5.0000   19.0000
    5.0000    1.4142    2.0000
    4.0000         0   15.0000
```



#### 3.2.4 截断和求余函数

![image-20210928205719857](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210928205739.png)

![image-20210928205734742](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210928205737.png)

例如，分别使用 fix() floor() ceil() round()，对向量A的每个元素进行截断运算

```matlab
>> A=[-1.55 -1.45 1.45 1.55];
>> Y=[fix(A) ; floor(A) ; ceil(A) ; round(A)]

Y =

    -1    -1     1     1
    -2    -2     1     1
    -1    -1     2     2
    -2    -1     1     2
```

例如，分别使用函数mod() rem()，对 -5/2 进行求余

```matlab
>> rem(-5,2)

ans =

    -1

>> mod(-5,2)

ans =

     1
```



## 第四章 基本编程

matlab可以进行程序设计，编写扩展名为.m的M文件，M文件的语法规则与C语言几乎一致

将有关 Matlab 命令编成程序存储在一个文件中（M 文件），然后在命令窗口中运行该文件，Matlab 就会自动依次执行文件中的命令，直到全部命令执行完毕

显示M文件内容，最简单的方法就是使用type命令

创建M文件，通过file → new → M-file

### 4.1 M文件基础

M文件有函数和脚本两种格式

#### 4.1.1 函数

function关键词为引导，定义函数名为test，输入参数x，输出参数y

注意函数名和文件名必须相同

![image-20211013210617214](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211013210620.png)例如，建立一个函数文件将变量a和b的值互换，然后在命令窗口调用该函数文件

![image-20211013210959650](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211013211001.png)

#### 4.1.2 脚本

可包含matlab的各种命令，类似于dos系统中批处理文件

前3章在命令窗口输入的每个代码或代码序列，都可以分别复制到新建M文件中然后保存为.m文件

运行方法：将脚本所在的目录设为当前的工作目录，debug菜单 → run



创建并运行脚本举例

![image-20211013211614795](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211013211617.png)

函数中的变量（特殊声明除外）都是局部变量，脚本的变量都是全局变量，驻留在matlab工作空间里，只要不关闭matlab，不使用clear清内存，这些变量将一直保存

### 4.2 变量和语句

#### 4.2.1 变量类型

必须以字母开头，之后可以是任意字母数字下划线

![image-20211013212103775](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211013212143.png)

全局变量的声明：global var1 var2

全局变量说明：

1. 使用前先定义，建议放在函数体的首行位置

2. 建议采用大写字母命名；

3. 全局变量会破坏程序的独立性，不利于模块化，不推荐使用

例如，创建脚本script2.m和function2.m

![image-20211013213053250](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211013213054.png)

![image-20211013213035235](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211013213037.png)

举例进一步理解全局变量：

![image-20211013213426058](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211013213428.png)

![image-20211013213500287](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211013213501.png)

![image-20211013213514156](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211013213516.png)



#### 4.2.2 程序控制结构

- **顺序结构**

  ![image-20211013214218792](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211013214221.png)

- **循环结构**

  for循环

  ```
  for 循环变量＝起始值:步长:终止值
  	循环体
  end
  ```

  例一

  ```matlab
  %求1+3+5+7+9
  %sum = 25
  
  clc
  sum=0;
  for i=1:2:10 
     	sum=sum+i;
  end
  sum
  ```

  例二

  ```matlab
  %求1！+2！+3！+ … +5！的值
  %sum = 153
  
  clc
  sum=0;
  for i=1:5
      pdr=1;
      for k=1:i
          pdr=pdr*k;
      end
      sum=sum+pdr;
  end
  sum
  ```

  while循环

  ```
  while 表达式
        循环体
  end
  ```

  例一

  ```matlab
  %求1到100和
  %sum = 5050
  
  clear
  sum=0; i=0;
  while i<100
  	i=i+1;
  	sum=sum+i;
  end
  sum
  ```

  

- **选择结构**

  if-else-end

  ```matlab
  if  表达式
      程序模块1
  elseif
      程序模块2
  elseif
      程序模块3
  else
      程序模块4
  end
  ```

  例如

  ```matlab
  clear
  n=input('输入n= '); 			
  if n>=90
      r='A'
  elseif n>=80
      r='B'
  elseif n>=70
      r='C'
  elseif n>=60
      r='D'
  else
      r='E'
  end
  ```

  switch-case-otherwise

  ```matlab
  switch  表达式
  	case 数值1
  		 程序模块1；
  	case 数值2 
  	     程序模块2；
  	otherwise
  		 程序模块n
  end
  ```

  例如

  ```matlab
  clear
  n=input('输入n= '); 
  switch fix(n/10)              
      case {10,9}
          r='A'
      case 8
          r='B'
      case 7
          r='C'
      case 6
          r='D'
      otherwise
          r='E'
  end
  ```

- **其他语句**

  break

  continue

  return

- **容错函数**

  error

  try-catch-end

- **时间运算函数**

  ![image-20211013220908611](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211013220911.png)

  ```matlab
  >> date
  
  ans =
  
      '13-Oct-2021'
  
  >> calendar
                     Oct 2021
       S     M    Tu     W    Th     F     S
       0     0     0     0     0     1     2
       3     4     5     6     7     8     9
      10    11    12    13    14    15    16
      17    18    19    20    21    22    23
      24    25    26    27    28    29    30
      31     0     0     0     0     0     0
      
  >> datevec('12/24/1984 12:45')
  
  ans =
  
          1984    12     24     12     45      0
  ```

- **人机交互命令**

  pause 等待用户反应 

  echo命令 

  input 用户输入提示 

  keyboard 请求键盘输入 

- **输出命令**

  disp

  ![image-20211013221502329](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211013221503.png)

  fprintf

  ```
  fprintf(fid,format,variables)
   %e ( 采用科学计算形式 )
   %f ( 采用浮点数形式 )
   %g ( 由系统自动选取上述两种格式之一 ) 
   %s ( 输出字符串 ) 
   %d ( 十进制数 ) 
   \n ( 换行 )  
   \t ( 制表符 ) 
   \b ( 退格 )  
   \\ ( 反斜杆 )    
   %% ( 百分号 ) 
  ```

  ![image-20211013221733617](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211013221735.png)



## 第五章 数据显示及存取

二维作图机制：先画点再连线

### 5.1 二维绘图

#### 函数plot()

plot(y)是基本二维绘图函数

y是向量：下标为横坐标，元素值为纵坐标

y是实数矩阵：分别绘制y的各列向量

y是复数向量：实部为横坐标，虚部为纵坐标

![image-20211020134004759](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211020134013.png)

![image-20211020134125302](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211020134126.png)



#### 函数plot(x,y)

x, y 都是向量：以 x 为横坐标， y 为纵坐标作平面曲线，x, y 必须具有相同长度。

x, y 都是矩阵：将 x 的列和 y 中相应的列相组合，绘制多条平面曲线，x, y 必须具有相同的大小

x 是向量, y 是矩阵：

若 x 的长度与 y 的行数相等，则将 x 与 y 中的各列相对应，绘制多条平面曲线

若 x 的长度与 y 的列数相等，则将 x 与 y 中的各行相对应，绘制多条平面曲线

 x 的长度必须等于 y 的行数或列数



例：y=cos(x) 在 [0, 4\*pi] 上的图像

![image-20211020134636156](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211020134637.png)



#### 函数 plot(x,y,string)

参数s为指定字符，代表不同的线性、点标和颜色

![image-20211020135025231](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211020135026.png)



例如：数据点选为菱形，连接曲线选为红色点画线

![image-20211020135522419](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211020135523.png)



#### 函数fplot()

fplot函数则可自适应地对函数进行采样，能更好地反应函数的变化规律

fplot函数格式：fplot(fname, lims, linespec)

fname为函数名，以@(x)f(x)形式出现，lims为变量取值范围，linespec定义绘图的线性、颜色等

例一

![image-20211020140537778](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211020140539.png)

例二

![image-20211020140457836](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211020140459.png)



#### 函数ezplot()

函数ezplot()用于绘制函数在某一自变量区域内的图形

1、ezplot(f): 绘制f=0在默认区域-2*pi<x<2*pi内的图形

2、ezplot(f,[min,max]): 绘制函数在区域min<x<max内的图形

3、ezplot(f,[xmin,xmax, ymin, ymax]): 绘制函数f(x,y)=0在区域xmin<x<xmax, ymin<y<ymax内的图形

![image-20211020140937039](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211020140938.png)



### 5.2 三维绘图

#### 函数plot3()

当x y z为长度相同的向量时，函数将绘制一条分别以 x0 y0 z0为 x y z轴坐标值的空间向量

当x y z都为mxn矩阵时，函数将绘制m条空间曲线

![image-20211020141732537](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211020141733.png)

#### 函数mesh()

绘制由矩阵 X,Y,Z 所确定的曲面网格图， C用于确定网格颜色，省略时随Z值成比例变化

X和Y必须均为向量，若X和Y的长度分别为m和n，则z必须为mxn矩阵

绘制由函数 z=z(x,y) 确定的曲面时，首先需产生一个网格矩阵，然后计算函数在各网格点上的值

```
网格生成函数：meshgrid
[X,Y]= meshgrid(x,y)
若 x = y, 则可简写为 
[X,Y]= meshgrid(x)
```

![image-20211020154421748](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211020154423.png)

绘制等高线 meshc()

![image-20211020154815936](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211020154817.png)

绘制边界面屏蔽 meshz()

![image-20211020154904803](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211020154906.png)



#### 函数surf()

surf(X,Y,Z)  绘制由矩阵 X,Y,Z 所确定的曲面图，参数含义同 mesh
mesh 绘制网格图，surf 绘制着色的三维表面图

![image-20211020155029513](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211020155030.png)



#### NOTE

.^ 2是矩阵中的每个元素都求平方，^2是求矩阵的平方或两个相同的矩阵相乘，因此要求矩阵为方阵

exp()与expm()的区别进行简单解释：

在matlab中exp(A) = e .^ A 表示矩阵A中的每个元素单独幂运算

expm(A) = e ^ A 表示对整个矩阵A进行幂运算

根据赵老师的要求，由于expm()大家目前没有接触，所以两种使用均可



### 5.3 图像处理

#### 图形标注

```
xlabel(’text’)
ylabel(’text’)
title('text', 'Property1',  value1,  ' Property2', value2, ...)
legend(string1,string2, ...)    %添加图例
text(x,y,string1,string2, ...)  %在指定坐标地方添加文本
axis([xmin, xmax, ymin, ymax, zmin, zmax])   %坐标轴的范围
```

![image-20211026174257335](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211026174258.png)





#### 划分区域指令

```
subplot(m,n,p) //将一个绘图窗口分割成 m*n 个子区域,p 表示第p个绘图子区域
linspace(a, b, n) //n是点的数目，即分成n-1等分，步长应当是(b-a)/(n-1) 
```

例子

```matlab
x=-pi:pi/10:pi;
subplot(2,2,1);plot(x,sin(x));
subplot(2,2,2);plot(x,cos(x));
subplot(2,2,3);plot(x,x.^2);
subplot(2,2,4);plot(x,exp(x));
```

![image-20211026175140284](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211026175142.png)

例子二

```matlab
x=linspace(0,2*pi,60);
y=sin(x);
z=cos(x);
t=sin(x)./(cos(x)+eps); %eps 为系统内部常数
ct=cos(x)./(sin(x)+eps);

%区域一
subplot(2,2,1); 
plot(x,y);
title('sin(x)');                 
axis ([0 2*pi -1 1]);  %控制坐标轴的刻度范围

%区域二
subplot(2,2,2);
plot(x,z);
title('cos(x)');
axis ([0 2*pi -1 1]);

%区域三
subplot(2,2,3);
plot(x,t);
title('tangent(x)');
axis ([0 2*pi -40 40]);

%区域四
subplot(2,2,4);
plot(x,ct);
title('cotangent(x)');
axis ([0 2*pi -40 40]);
```

![image-20211026180058126](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211026180059.png)



例子三，重新绘制上例4个图形，程序变动后如下

```matlab
x=linspace(0,2*pi,60);
y=sin(x);
z=cos(x);
t=sin(x)./(cos(x)+eps);   
ct=cos(x)./(sin(x)+eps);

H1=figure; %创建新窗口并返回句柄到变量H1
plot(x,y); %绘制图形并设置有关属性
title('sin(x)');           
axis ([0 2*pi -1 1]);  

H2=figure;%创建第二个窗口并返回句柄到变量H2
plot(x,z); %绘制图形并设置有关属性
title('cos(x)');
axis ([0 2*pi -1 1]);

H3=figure; %同上
plot(x,t);
title('tangent(x)');
axis ([0 2*pi -40 40]);

H4=figure; %同上
plot(x,ct);
title('cotangent(x)');
axis ([0 2*pi -40 40]);
```

发现一共有4个figure

![image-20211026180433202](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211026180434.png)



#### 其他指令

```
grid on 显示网格
grid off 不显示网格
hold on 保持当前窗口图像
hold off 不保持
figure(n) 新建绘图窗口
```

grid on / grid off 举例

![image-20211026174605714](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211026174607.png)

hold函数举例

```matlab
x=linspace(0,2*pi,60);
y=sin(x);
z=cos(x);
plot(x,y,'b');       % 绘制正弦曲线
hold on;             % 设置图形保持状态
plot(x,z,'g');       % 保持正弦曲线同时绘制余弦曲线
axis([0 2*pi -1 1]);     
legend('cos','sin');
hold off             %关闭图形保持
```

![image-20211026181029453](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211026181030.png)

同时绘制多个函数图像

```matlab
plot(x1,y1,s1,x2,y2,s2, ... ,xn,yn,sn)
等价于
hold on
plot(x1,y1,s1)
plot(x2,y2,s2)
...
plot(xn,yn,sn)
```



## 第六章

### 6.1 多项式运算

#### 1.多项式主要函数

![image-20211102213719063](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211102213727.png)

#### 2.多项式的表示法

![image-20211102214119537](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211102214120.png)

```
>> A=[1 3 0 4 5];
>> [s, len]=poly2str(A,'x')

s =
    'x^4 + 3 x^3 + 4 x + 5'
len =
    24
len为字符串s的长度，‘x’表示字符串中变量用x表示
```

#### 3.多项式求值

```matlab
y = polyval(p,x) %计算多项式 p 在 x 点的值，矩阵则采用点运算
y = polyvalm(p,x) %矩阵多项式求值，x必须是方阵

%区分两个函数
polyvalm(p,A) = 2*A*A*A - A*A + 3*eye(size(A)) 
polyval(P,A) = 2*A.*A.*A - A.*A + 3*ones(size(A))
```

```matlab
>> p=[2,-1,0,3];
>> x=2; y=polyval(p,x)

y =
    15

>> x=[-1, 2;-2,1]; y=polyval(p,x)

y =
     0    15
   -17     4
   
```

```matlab
>> p=[2,-1,0,3];
>> x=[-1, 2;-2,1];polyval(p,x)

ans =
     0    15
   -17     4

>> polyvalm(p,x)

ans =
    12   -12
    12     0
```

#### 4.多项式加减运算

```
k = conv(p,q)  %多项式乘法
[k,r] = deconv(p,q) %多项式除法，k返回的是多项式 p 除以 q 的商，r 是余式
```

```
>> p=[2,-1,0,3];
>> q=[2,1];
>> k=conv(p,q)

k =
     4     0    -1     6     3
```

#### 5.多项式微积分（求导）

```
k=polyder(p)     %多项式 p 的导数；
k=polyder(p,q)   %p*q 的导数；
[k,d]=polyder(p,q)  %p/q 的导数，k 是分子，d 是分母
```

```matlab
>> k1=polyder([2,-1,0,3])

k1 =
     6    -2     0
     
>> k2=polyder([2,-1,0,3],[2,1])

k2 =
    16     0    -2     6

>> [k2,d]=polyder([2,-1,0,3],[2,1])

k2 =
     8     4    -2    -6
d =
     4     4     1
```

#### 6.多项式的不定积分

```
polyint(p,n) %n表示常数项，默认0
```

```
>> p1=[1 2 3];
>> s1=polyint(p1)

s1 =
    0.3333    1.0000    3.0000         0

>> s2=polyint(p1,2)

s2 =
    0.3333    1.0000    3.0000    2.0000
```

#### 7.多项式的根及由根创建多项式

```
x=roots(p) %若 p 是 n 次多项式，则输出是 p=0 的 n 个根组成的 n 维向量
p=poly(x)  %若已知多项式的全部零点，则可用 poly 函数给出对应多项式
```

```
>> p=[2,-1,0,3]; 
>> x=roots(p)

x =

   0.7500 + 0.9682i
   0.7500 - 0.9682i
  -1.0000 + 0.0000i
```

```
例如：由根[-2 2 1]创建多项式
>> r=[-2 2 1];
>> p=poly(r);
>> sp=poly2str(p,'x')

sp =

    'x^3 - 1 x^2 - 4 x + 4'
```



#### 8.多项式部分分式展开

![image-20211102225000348](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211102225001.png)

```
在上图中，令
num=[b0  b1 … bn]
den =[1 a1 … an]

用residue()函数求B(s)/A(s)的部分分式展开式
[num  den] = residue(r, p, k)
[r  p  k] = residue(num, den)
```



例如 :试求下列函数的部分分式展开式 

![image-20211102225313674](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211102225314.png)

```
>> num = [1 11 39 52 26];
>> den = [1 10 35 50 24];
>> [r,p,k]=residue(num,den)

r =

    1.0000
    2.5000
   -3.0000
    0.5000


p =

   -4.0000
   -3.0000
   -2.0000
   -1.0000


k =

     1
```

所以最后的结果是

![image-20211102225947541](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211102225948.png)

#### **9.多项式曲线拟合**

用polyfit函数来求得最小二乘拟合多项式的系数，再用polyval函数按所得的多项式计算所给出的点上的函数近似值

```
[P,S]=polyfit(x,y,m)  根据采样点X和函数值Y，产生一个m次多项式P及其在采样点的误差向量S
polyval(P,x) 函数的功能是按多项式的系数计算x点多项式的值
```

下面是一个例题

```matlab
>> x=0:0.1:1;       %11个点
>> y=[-0.447 1.978 3.28 6.16 7.08 7.34 7.66 9.56 9.48 9.30 11.2];
>> a=polyfit(x,y,2)

a = -9.8108   20.1293   -0.0317

>> z=polyval(a,x)

z =
   -0.0317    1.8831    3.6018    5.1241    6.4503    7.5803    8.5140    9.2515    9.7928   10.1379    10.2868

>> plot(x,y,'r*',x,z,'b')
```

![image-20211102230954789](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211102230956.png)

### 6.2 插值运算

插值是根据已知输入/输出数据集和当前输入估计输出值

![image-20211102231836816](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211102231838.png)

#### 1. 一维数组插值

```matlab
Y1=interp1(X,Y,X1,'method')

函数根据X,Y的值，计算函数在X1处的值。X,Y是两个等长的已知向量，描述数据点，X1是一个向量或标量，描述欲插值的点，Y1是一个与X1等长的插值结果

method是插值方法有：
'nearest'  最邻近插值
'linear'   默认方法，线性插值
'spline'   三次样条插值

补充三种插值方法：
最邻近：返回已知数据集中与当前输入最邻近点对应的输出
线性：返回当前输入与他相邻两点直线上的取值，对应的输出
三次样条：返回当前输入在采用三次样条函数上的取值
```

以下是例题

```matlab
x=0:1.2:10;
y=sin(x);
xi=0:0.1:10;
yi_nearest=interp1(x,y,xi,'nearest');
yi_linear=interp1(x,y,xi);
yi_spline=interp1(x,y,xi,'spline');

figure;
hold on;
subplot(1,3,1);
plot(x,y,'ro', xi, yi_nearest, ' b-' );
title('最临近插值');
subplot(1,3,2);
plot(x,y,'ro', xi, yi_linear, ' b-' );
title('线性插值');
subplot(1,3,3);
plot(x,y,'ro', xi, yi_spline, ' b-' );
title('三次样条插值');
```

结果如图：

![image-20211103135204127](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211103135205.png)

#### 2. 二维数组插值

```
Z1=interp2(X,Y,Z,X1,Y1,'method')

X,Y是两个向量，分别描述两个参数的采样点，Z是与参数采样点对应的函数值
X1,Y1是两个向量或标量，描述欲插值的点。Z1是根据相应的插值方法得到的插值结果
```

下面是二维插值的例子

```matlab
[x,y]=meshgrid(-3:0.8:3);
z=peaks(x,y);
[xi,yi]= meshgrid(-3:0.25:3);
zi_linear=interp2(x,y,z,xi,yi);
zi_nearest=interp2(x,y,z,xi,yi,'nearest');
zi_spline=interp2(x,y,z,xi,yi,'spline');

figure;
hold on;

subplot(2,2,1);
meshc(x,y,z);
title('原始数据');

subplot(2,2,2);
meshc(xi,yi,zi_nearest);
title('最临近插值');

subplot(2,2,3);
meshc(xi,yi,zi_linear);
title('线性插值');

subplot(2,2,4);
meshc(xi,yi,zi_spline);
title('三次样条插值');
```

![image-20211103135844385](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211103135845.png)
