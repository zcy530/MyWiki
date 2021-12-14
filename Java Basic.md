面向对象的三大基本特性：封装、继承、多态

### 第二章 java环境搭建

编写：利用记事本/IDE完成代码文件 (.java) 的编写

编译：利用JDK中 javac.exe 将代码文件 (.java) 编译为字节码文件 (.class)

运行：java.exe读入并解释字节码文件 (.class)，最终在JVM上运行

![image-20210705142035099](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210705142035099.png)



Eclipse和java(JDK, JRE, JVM) 之间的关系

eclipse相当于帮我们管理很多java和class文件，给我们提供一个友好的界面，让我们更容易的写.java文件，.java要依靠JDK里面的 javac.exe来编译，编译完成后会产生一个.class文件，.class文件要继续调用JRE里面的java.exe来运行，JRE运行的时候里面会自动生成一个JVM(java virtual  machine)

![image-20210705145705235](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210705145705235.png)



java程序三种错误：语法错误，运行错误，逻辑错误



### 第三章  Java类基础知识

#### 3.1 java类结构

类是java最基础的逻辑单位

java中所有的内容都是需要放在类的范围内，不允许游离在类以外

一个java文件里可以有多个class，但是只能有一个public class

一个class最多只能有一个main函数，是程序的入口，也可以没有main函数，没有main函数的类不能主动执行，但可以被动调用执行，main函数的形参和前缀修饰符都不能省略，public static void main(String[] args) 是固定写法

main函数不算成员函数，无法被其他方法和类调用

```java
System.out.print()
System.out println() //换行输出

import java.util.Scanner;
Scanner input=new Scanner(System.in);

int score=input.nextInt(); //输入整数
String name = in.nextLine();//读取一行字符串，中间可以有空格
String firstName = in.next();//读取一个字符串，中间没有空格
double d = in.nextDouble();//读取一个double类型的数据 
```

#### 3.2 基本数据类型和运算符

**Java标识符(identifiers)规定：**

以字母、下划线、美圆符开始的一个字符序列

除开始的第一个字符外，后面可跟字母、下划线、美圆符和数字

标识符区分大小写

没有长度限制

不能与保留字(reserved word)或关键字(keyword)相同



**数据转换**：

低精度的数据类型在运算过程中可以自动转换为高精度的数据，而高精度的数据需要经过强制转换才能够变成低精度的数据

(1)整型,实型,字符型数据可以混合运算。运算结果的精度由表达式中精度最高的变量决定

```java
double d=15.3; int i=30;
d=d+i //结果是一个double型的变量
i=d+i // error，结果是double型的不能够赋值int型的变量
```

(2)byte和short型的数据参加运算时会自动变为int类型

(3) 在byte或者short的取值范围内时可以直接赋值给一个byte或者short类型的变量。反之，必须要通过强制类型转换来赋值

```java
int i=10;
byte b=(byte)i; //用变量i来给变量b赋值时，需要强制转换。
long d=10；
int j = d；//error
int j = (int)d；
```

![image-20210715062344762](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210715062344762.png)

![image-20210715062614493](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210715062614493.png)



boolean 只有true和false两个值

int, long 定义时末尾要加L

double 8个字节, float 4个字节 定义时末尾必须要加f

char是一个单一的16位unicode字符，\u4e00-\u9fa5两万多汉字

运算符：+ - * / % && || ! != > >= < <=

#### 3.3 选择和循环结构

if...else  if...else if...else

switch

while  do...while

for

break：中断循环并退出

continue：结束本次循环，进入下一次循环，本次循环余下代码不做

调试设断点，然后右键debug as java application

step into下一句，step over 执行system.out.print时

#### 3.4 自定义函数

修饰词 + 返回值 + 函数名 （形参）{函数体}

overload函数重载：函数名可以相同，但是其<u>参数的个数、类型、顺序</u>有所不同，不能通过返回值来区别重载函数，不能有两个名字相同，参数类型也相同，却返回不同类型值的方法。



### 第四章 面向对象

#### 4.1 面向对象思想

对象 = 属性 + 方法

变量定义的变迁：基本类型 -> 结构体 -> 类

#### 4.2 java类和对象

```java
class A{}
A obj1 = new A()
A obj2 = new A()
//obj1, obj2指针指向不同的内存
obj1 = obj2
//赋值以后obj1, obj2指针指向相同的内存
```

对象赋值时reference，就是指针变换，基本类型的赋值是直接值拷贝



对象初始化：

函数内的局部变量，编译器不会给默认值，需要初始化才能使用

类的成员变量，编译器会给默认值，可以直接使用



对象与引用：

引用只有被初始化之后（指向对象空间时），才能够被调用

```java
Book b1,b2,b3; //引用 reference
b1 = new Book(); //ok
b2 = b1;//ok
b3 = new Student()//error, b3需要指向book类型的对象空间
```

引用的赋值运算的结果是：两个引用指向同一个对象空间。一个对象空间拥有的引用数目不受限制

#### 4.3 构造函数

构造函数名称和类名一样，且没有返回值

java有构造函数，没有析构函数，JVM会自动回收所分配的变量的内存

每个变量都是有生命周期的，都只能存活在离它最近的大括号里面

每个子类的构造函数第一句话，都默认调用父类的无参构造函数super()，除非子类的构造函数第一句话就是super()

可以有多个构造函数

#### 4.4 信息隐藏和this

类的成员属性是私有的，private

类的方法是共有的，public

信息隐藏：通过类的方法来间接访问类的属性，而不是直接访问类的属性

可以通过IDE自动产生get和set方法

![image-20210708160126677](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210708160126677.png)

![image-20210708160202868](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210708160202868.png)



this负责指向本类中的成员变量

this负责指向本类中的成员方法

this可以代替本类中的构造函数

![image-20210708160552484](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210708160552484.png)

静态方法体中不能使用this关键字

静态方法体中不能使用this关键字访问静态属性

非静态方法中可以用this关键字访问静态属性

![image-20210715064001389](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210715064001389.png)

### 第五章 继承、接口、抽象类

#### 5.1 继承

class Son extends Father

![image-20210708160940497](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210708160940497.png)

子类继承父类，父类的父类，所有的属性和方法，但不能直接访问private成员

子类可以通过调用父类的方法来访问父类的私有的成员属性

单根继承原则：每个类都只能继承一个类

如果构造函数的第一句话不是super，编译器会自动增加一句super()，如果构造函数第一句是程序员自己写的super语句，编译器就不会自动增加了

#### 5.2 抽象类和接口

一个完整的类：所有的方法都实现了，类可以没有方法，但是有方法就一定要实现，这才是一个完整的类

一个完整的类才能被实例化，被new出来

如果一个类暂时还有方法没有实现，被定义为**抽象类abstract**

```java
public abstract class{
    int area;
    public abstract void calArea();
}
```

特点：

一个类继承于抽象类，就不能继承于其他的抽象类

子类继承抽象类，如果不能完全实现父类的所有abstract方法，那么子类也必须被规定为抽象类



如果一个类中所有方法都没实现，那么这个类就算是**接口interface**

```java
public interface Animal{
    public void eat();
    public void move();
}
```

一个类只能继承extends一个类，但是可以实现implements多个接口

一个接口可以继承多个接口，关键字用extends

类实现接口，就必须实现所有未实现的方法，否则是抽象类

```java
public abstract LandAnimal implements Animal{
    public abstract void eat();
    public void move(){
        System.out.print("move");
    }
}
```



抽象类有构造函数，接口没有构造函数

抽象类可以有private/protected，接口必须是public

#### 3. 转型、多态、契约

子类可以转换为父类，而父类不可以转换为子类

子类继承父类所有的财产，子类可以变成父类(从大变小，即向上转型)

从父类直接变成子类(从小变大，即向下转型)，则不允许

```java
Human obj1 = new Man(); //OK
Man obj2 = new Human(); //illegal
```

父类转为子类有一种情况例外，就是这个父类本身就是从子类转化过来的

```java
Human obj1 = new Man();
Man obj2 = (Man) obj1;
```



overwrite/override：子类继承父类的所有方法，但子类可以重新定义一个名字、 参数和父类一样的方法，子类优先级高于父类

![image-20210714190911133](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714190911133.png)

三个obj指向同一块内存，调用的eat()都是子类的



**多态**：子类转型为父类后，调用的普通方法，依旧是子类本身方法

多态的作用：

以统一的接口来操纵某一类中不同的对象的动态行为 

对象之间的解耦



**契约**：规定规范了对象应该包含的行为方法

类不会直接使用另外一个类，而是采用接口的形式，外部可以“空投”这个接口下的任意子类对象



### 第六章 static、final、常量设计

#### 1. static

**静态变量**：

类共有成员，可以依赖于类存在，不依赖于对象实例存在，即可以在main中用 类.变量名访问

在内存里只有一个，所有的对象实例这个变量，都存储在同一个内存空间里

![image-20210714192750482](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714192750482.png)

**静态方法**：

静态方法也无需通过对象来引用，而通过类名可以直 接引用

在静态方法中，只能使用静态变量，不能使用非静态变量

静态方法禁止引用非静态方法，非静态方法可以<u>直接引用</u>静态方法

![image-20210714193142370](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714193142370.png)



静态代码块：

只在类第一次被加载时调用。 

换句话说，在程序运行期间，这段代码只运行一次

执行顺序：static块 > 匿名块 > 构造函数

![image-20210714193340090](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714193340090.png)

![image-20210714193419792](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714193419792.png)

![image-20210714193453351](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714193453351.png)



使用static关键字记录创建了多少个对象：

```java
class Emp {
    static int count = 0;
    String name;
    public Emp(String name) {
        this.name = name;
        count++;
    }
    public Emp() {
        count++;
    }
}
public class ConstructStatic {
    public static void main(String[] args) {
        Emp e1 = new Emp();
        Emp e2 = new Emp();
        Emp e3 = new Emp("zhangshan");
        System.out.println("创建了" + Emp.count + "个对象");
    }
}
```



#### 2. 单例模式

限定某一个类在整个程序运行过程中，只能保留一个实例对象在内存空间

采用static 来共享对象实例 

采用private 构造函数，防止外界new操作

![image-20210714194216756](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714194216756.png)

![image-20210714194247263](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714194247263.png)

双等号：指针相等



#### 3. final

final类：不能被继承

```java
final public class Father{
}
class son extends Father{
}//Error
```

final方法：父类中如果有final的方法，子类中不能改写此方法

final变量：不能再次赋值

如果是基本型别的变量，不能修改其值

如果是对象实例，那么不能修改其指针(但是可以修改对象内 部的值

```java
final int a = 5;
a = 10;// Error

public class FinalObj{
    int a = 10;
    public static void main(String[]){
        final FinalObj obj = new FinalObj();
        obj.a = 20;//OK
        obj = new FinalObj();//Error
    }
}
```



#### 4. 常量设计和常量池

Java没有constant关键字

Java中的常量：public static final

![image-20210714195801545](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714195801545.png)

一种特殊的常量：接口内定义的变量默认是常量

![image-20210714195844004](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714195844004.png)



常量池：相同的值只存储一份，节省内存，共享访问

基本类型的包装类 ：Boolean，Byte，Short，Integer，Long，Character，Float，Double 

Boolean： true, false 

Byte, Character : \u0000--\u007f (0—127) 

Short, Int, Long：-128~127 

Float，Double：没有缓存(常量池)

![image-20210714201247081](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714201247081.png)



java为<u>常量字符串</u>都建立常量池缓存机制

![image-20210714201704194](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714201704194.png)



基本类型的包装类和字符串有两种创建方式，这两种创建方式导致创建的对象存放的位置不同

1. 常量式(字面量)赋值创建，放在栈内存 (将被常量化) 

   ```java
   Integer a = 10; 
   String b = "abc"; 
   ```

2. new对象进行创建，放在堆内存 (不会常量化) 

   ```java
   Integer c = new Integer(10); 
   String d = new String("abc");  
   ```

举例1：

![image-20210714202232334](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714202232334.png)

![image-20210714202542879](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714202542879.png)

举例2：

![image-20210714202936693](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714202936693.png)



#### 5. 不可变类型

不可变对象(Immutable Object) ：一旦创建，这个对象（状态/值）不能被更改了，其内在的成员变量的值就不能修改了

典型的不可变对象 ：

八个基本型别的包装类的对象 ，String，BigInteger和BigDecimal等的对象



![image-20210714203428527](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714203428527.png)

![image-20210714203514101](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714203514101.png)

不可变对象，也是传指针(引用) 

由于不可变，临时变量指向新内存，外部实参的指针不改动



#### 6. String

字符串内容比较：equals方法 

是否指向同一个对象：指针比较==

StringBuffer/StringBuilder 的对象都是可变对象 

StringBuffer(同步，线程安全，修改快速)

StringBuilder(不同步，线程不安全，修改更快)

![image-20210714204222264](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714204222264.png)



### 第七章 package、import

#### 1. package

Note: 

1.文件所在的目录必须要与其包名一致。否则虽然编译能通过但是运行不能通过

 2. 运行class文件时前面需要加上所在包名，否则不能运行

#### 2. 访问权限

类的访问权限修饰符：只能是public和friendly(缺省)

属性：[public | protected | private] [static] [final]

方法：[public | protected | private] [static] [final | abstract］

![image-20210714205413103](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714205413103.png)

![image-20210714205405545](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714205405545.png)

![image-20210715034030171](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210715034030171.png)



### 第八章 java常用类库

#### 1. 数字类

java.lang.Math

Math类中的方法都是静态方法所以通过类名直接访问

```java
public static int abs(int a) //Math.abs();
public static double ceil(double d)
public static double floor(double d)
public static int round(float f)
public static long round(double d) //Math.round(-10.5)
public static int max(int a, int b) //x = Math.max(1024, -5000);
public static int min(int a, int b)
public static double pow(double a, double b) //a的b次幂
public static double exp(double d) //求Math.E的d次幂
```

#### 2. 字符串类



#### 3. 时间类

#### 4. 格式化类

对话框：

```java
import javax.swing.*;
public class InputTest2 {
    public static void main(String[] args) {
        String name = JOptionPane.showInputDialog("What is your name?");
        String input = JOptionPane.showInputDialog("How old are you?");
        int age = Integer.parseInt(input);//类型转换
        System.out.println("Hello," + name + ". Next year, you'll be " +(age + 1));
        System.exit(0); 
    } 
}
```

printf:

```java
System.out.printf("%,.2f",10000.0 / 3.0); //按照浮点数格式输出，整数位用逗号分割，小数位为2位
System.out.printf("%tc",new Date());//%tc表示：t是日期输出的提示，c表示输出完整的日期
System.out.printf(“%1$s %2$tB %2$te, %2$tY”,“Due date:”,new Date());
%1$s表示：第一个参数即“Due date:”按照字符串来输出
%2$tB表示：第二个参数即“new Date()”输出英文的月
%2$te表示：第二个参数即“new Date()”输出两位数字日
%2$tY表示：第二个参数即“new Date()”输出四位数字年
```

java.text.Format:

日期：DateFormatter、SimpleDateFormat

数字：NumberFormat、DecimalFormat

字符串：MessageFormat

```java
import java.text.Format.NumberFormat
NumberFormat N = NumberFormat.getInstance();
System.out.println(1000/3.0 + " " + 10000);
System.out.println(N.format(1000/3.0) + " " + N.format(10000));
输出为：
333.3333333333333 10000
333.333 10,000
    
NumberFormat C = NumberFormat.getCurrencyInstance();
System.out.println(C.format(1000));
C = NumberFormat.getCurrencyInstance(Locale.US);
System.out.println(C.format(1000));
输出为：
￥1,000.00
$1,000.00
```

```java
import java.text.Format.DecimalForma
double avprice="28234.2534";
DecimalFormat df =new DecimalFormat("#.00");
String aveprice=df.format(avprice);
//整数保留不变，后面保留2位小数，不足则补0
```

![image-20210715070626732](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210715070626732.png)



![image-20210715065818464](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210715065818464.png)

![image-20210715065718523](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210715065718523.png)

java.time.Format:



### 第九章 异常处理

ArithmeticException: 除以零

ArrayIndexOutOfBoundException: 数组越界

FileNotFoundException: 打开不存在的文件

整数溢出、浮点数溢出、硬件错误、使用了不可用了IO设备等

```java
int[] br = new int[6];
try {
    System.out.println(br[10]);
}catch(Exception e) {
    System.out.print(e.getMessage());
}

//result：Index 5 out of bounds for length 6
```

异常可以理解为一个特殊的类

捕获并且处理异常的格式：

```java
try{
	......
}catch(SomeExceptionType e){
	......
}catch(Exception e){
	......
}
```

如果try没有异常，catch直接跳过

如果异常第一个不匹配，就一直往下走

如果到最后还是没有匹配到错误类型就还是会报错



**finally**：

一定会执行的程序块

```java
try{
    ......
}
catch(){
    ......
}
finally{
    //无论发生什么异常，或者不发生异常，或者在try里直接return了，都会执行的部分
}
```

finally{}代码段在某些情况下是非常有用的，例如在异常发生之后我们还需要务必关闭数据库的连接，关闭文件，关闭已经打开的端口，关闭网络连接等



**Java常用的异常类：** 

 RuntimeException： 

错误的转型（cast）：java.lang.ClassCastException 

数组越界错误：java.lang.ArrayIndexOutOfBoundsException 

空指针错误：java.lang.NullPointerException 

数组元素类型错误：java.lang.ArrayStoreException 

算术运算错误：java.lang.ArithmeticException 

String转换成数字类型时的错误： java.lang.NumberFormatException 

非RuntimeException: 

文件读取越界：java.io.EOFException 

文件没有找到：java.io.FileNotFoundException 

URL链接错误：java.net.MalformedURLException 

主机不可识别：java.net.UnknownHostException



**Exception类中的构造函数:** 

```java
public Exception();
public Exception(String message);
```

**throw：**

一般与异常对象关联，我们可以在程序中需要的位置 自己抛出异常

如果程序执行中遇到了throw语句则正常的流程中断，转入到catch程序块中处理异常。

```java
NullPointerException ex = new NullPointerException()
throw ex;
```

如何得到异常描述信息：

在Exception的父类Throwable（java.lang包）中有定义

```java
String getMessag();
String toString();
Void printStackTrace();
```

```java
throw new Exception("Here's my Exception");

/* result 打印的内容是throw里面写的内容
e.getMessage(): Here's my Exception
e.toString(): java.lang.Exception: Here's my Exception
e.printStackTrace():java.lang.Exception: Here's my Exception at ExceptionMethods.main(ExceptionMethods.java:4)  
*/
```



一般来说在一个方法的内部出现异常时，可以有两种处理方法： 

1. 在方法的内部异常出现的地方，即throw语句出现的地方，用try语句捕获异常，catch语句处理异常。 

2. 产生异常的方法不直接处理异常而是由<u>调用该方法的其他方法</u>来用try和catch程序块处理异常。

   ```java
   public class Test{
       public void division(){
           int num1 = 10;
           int num2 = 0;
           if(num2==0)
               throw new ArithmeticException();
           System.out.println(num1 / num2);
       }
       public static void main(String[] args) {
           Test t = new Test();
           try{
               t.division();
           }catch(ArithmeticException e){
               ......
           }
       }
   }
   ```



**使用自定义的异常：**

定义异常：

自定义的异常一般是Java系统中标准的Java Exception类或Throwable类的子类或者是你已经定义好的异常类的子类

```java
public class YourNewException extends Exception {}

class NotAValidAttribute extends Exception{
    public NoValidAttribute(){}
    public NoValidAttribute(String err){
        super(err);
    }
} 
```

抛出异常：throws ,throw

1. 在方法名称后首先定义方法中将要抛出的异常类型列表

   throws语句位于方法头部的后面，用来声明方法内部已经抛出的并且还没有用try和catch程序块处理的异常的类型

2. 在需要报告异常的部分，创建相应的异常的实例，并且throw出该实例

```java
public void setName(String n) throws NotAValidAttribute {
    if (n == null)
        throw new NotAValidAttribute("employee's name is null");
    else
        name = n;
} 
```



捕获异常：try，catch，finally

```java
try{
    ......
}
catch(MyExceptionType1 e){
    ......
}
catch(MyExceptionType2 e){
    ......
}
```

```java
class NotAValidAttribute extends Exception{
	public NotAValidAttribute (){}
	public NotAValidAttribute (String err){
	super(err);}
}

public class employee{
    private String name;
    private int age;

    public employee(){}
    public employee(String n, int a) throws NotAValidAttribute {
        this.setName(n);
        this.setAge(a);
    }
    public void setName(String n) throws NotAValidAttribute{
    	name=n;
    }
    public void setAge(int a) throws NotAValidAttribute{
        if( a <= 18 || a >70)
            throw new NotAValidAttribute("error: employee's age must between 18 to 70");
        else age = a;
    }

    public static void main(String args[]){
        try{
            employee emp1 = new employee("Zhangcaiyi", 16);
        }catch (NotAValidAttribute e){
            System.err.println(e.getMessage());}
    }
}
```

该构造方法调用的setName，setAge等方法都抛出了自己的异常，而构造方法可以不在此时对这些异常处理，这种情况 下可以直接利用throws将异常抛出，留给后面的 调用该构造方法的main来处理异常（try-catch）



### 第十章 数据结构

Array & ArrayList

存放相同类型的变量组合

定义方法：

```java
int arrayname[];
int[] arrayname; //如果是局部变量不会自动初始化
public static int[] arrayname; //如果是属性，系统自动生成化为null

int[] arr = new int[4]; //定义并产生了由4个int组成的数组空间，初始化0，boolean类型为false
Car[] cars = new Car[6]; //定义并产生了由6个Car对象组成的数组空间，初始化null
```

初始化：

1. 使用循环语句

2. 统一初始化

   ```java
   Car[] cars = {new Car(),new Car()};
   int[] arr = {1,2,3}
   ```

3. 动态统一初始化

   ```java
   Car[] cars = new Car[]{new Car(),new Car()};
   ```

赋值：

java数组名也是引用，相同类型的数组名之间可以进行赋值操作

```java
public class ArrayTest1 {
	public static int[] ar = new int[5];
	public static void main(String[] args) {
		int[] br = new int[6];
		br=ar;
		System.out.println(ar);
		System.out.println(br);
	}
}
//result，说明赋值之后内存空间是一样的
[I@2d363fb3
[I@2d363fb3
```

读取长度：arr.length

二分查找：看代码

对于基本类型、封装类、String类的数组可以调用java中array静态方法binarySearch直接完成查找

排序：看代码

复制：

1. 两个变量引用相同数组，指向相同的地址

   ```java
   Car[] cars = new Car[5];
   for(int i=0,i<cars.length,i++)
       cars[i]=new Car();
   Car[] carsCopy = cars;
   ```

2. 复制到另外的数组，指向不同的地址

   ```java
   System.arraycopy(fromArr,fromIndex,toArr,toIndex,count);
   System.arraycopy(cars,2,carCopy,0,3);
   //把cars从第2个下标开始，共3个元素，分别复制到carCopy空间从0-2处
   ```



数组可以作为用户自定义方法的参数

数组作为参数传入方法实际传入的是数组的引用，故Java中的方法可以改变数组中的元素的值。方法的返回值类型可以作为一个数组。 Java中返回的是一个数组的引用，指向一个array

```python
public class ArrTest {
	private Car[] cars=new Car[] {new Car(), new Car()};
	private String[] arr ={"abc","def","ghi","lnn"};
	private int[] arrInt = {11,45,66,89};
	private void changeValue(String[] str, int i){
		System.out.println("before change：String[]:"+arr[i]);
		str[i] = "changed";
		System.out.println("After change：String[]:"+arr[i]);
	}
	private void changeValue(Car[] car_, int i){
		System.out.println("before change Car[]'sname:"+cars[i].carName);
		car_[i].carName ="red flag";
		System.out.println("After change Car[]'sname:"+cars[i].carName);
	}
	private void changeValue(int[] arrInt_,int i){
		System.out.println("before changeint[]:"+arrInt[i]);	
		arrInt_[i] =100;	
		System.out.println("after changeint[]:"+arrInt[i]);
	}
	
	public static void main(String[] args){
		ArrTest arrArg = new ArrTest();
		arrArg.changeValue(arrArg.arr,2);
		arrArg.changeValue(arrArg.cars,1);
		arrArg.changeValue(arrArg.arrInt,3);}
}
//result
before change：String[]:ghi
After change：String[]:changed
before change Car[]'sname:null
After change Car[]'sname:red flag
before changeint[]:89
after changeint[]:100
```



### 第十一章 文件读写

#### 1. 文件 java中的file类

java的文件和目录都用file类，封装了对操作系统文件操作的功能

构造函数：

```java
File(String pathname)
File(String directoryPathname, String filename)
File(File directory, String fileName)
File(URI ur)
```

创建对象：

```java
File f=new File("D:\\mytest\\text.txt");
File f=new File("D:"+ File.separator +"mytest"+ File.separator +"test.txt");
```

抛出异常：

IOException

SecurityException

常用方法：

```java
import java.io.*

String getName()  返回文件名，不包括路径信息
String getPath()  返回文件的路径名
String getAbsolutePath()  返回绝对路径名。
long lastModified()  返回最后修改的时间
long length()  返回文件的长度
    
//文件或者目录的判断
boolean exists()       判断文件是否存在
boolean isFile()       判断是否为文件
boolean isDirectory()  判断是否为目录
    
//文件的读写判断
boolean canRead()   文件是否可读
boolean canWriter() 文件是否可写

//创建新的文件
boolean createNewFile() throws IOException 当文件不存在时，调用该方法创建新的文件
boolean mkdir()   创建一个由该文件对象指定的子目录
boolean mkdirs()  创建由该文件对象指定的目录
    
//文件属性的修改
boolean renameTo(File dest)：重命名
boolean setReadOnly():设置文件只读
    
//获取目录中的文件信息
String[] list(),如果file对象为一个目录，返回这个文件对象所包含的文件及子目录的名字。如果为一个文件则返回空(null)
File[] listFiles(),如果file对象为一个目录，返回这个文件对象所包含的文件及子目录构成的对象数组。如果为一个文件则返回空(null) 
```

例子：

```java
//目录
File d = new File("E:\\temp");
if(!d.exists()) 
    d.mkdirs();
System.out.println(d.isDirectory());
//文件
File f = new File("E:\\temp\\test.txt");
if(!f.exists())
    try {
        f.createNewFile();
    } catch (IOException e) {
        e.printStackTrace();
    }
System.out.print(f.isFile());
//打印子列表
File[] fs = d.listFiles();
for(File i:fs) 
    System.out.println(i.getPath());
```



#### 2. 流 Stream

java读写文件，只能以数据流的形式

File类和Stream类的区别：

 File类主要用来描述系统中的文件在磁盘上的<u>存储情况</u>

Steam类主要是对<u>文件的内容</u>进行操作



#### 3.java IO包

节点类：直接操作文件类

InputStream：按照字节读取 FileInputStream子类

OutputStream：按照字节输出 FileoutputStream子类

Reader：按字符读取 FileRreader子类

Writer：按字符输出  FileWriter子类



转换类：字符到字节的转换

InputStreamReader 字节->字符

OutputStreamReader 字符->字节



装饰类：装饰节点类

DataInputStream, DataOutputStream

BufferInputStream, BufferOutputStream 缓存字节流

BufferReader, BufferWriter  缓存字符流

#### 

system类中的三类标准数据流：

```java
public static final InputStream in;//标准输入流
public static final PrintStream out;//标准输出流
public static final PrintStream err; //错误流
```

当在print方法的参数中传递的是一个对象时，系统将会调用该对象的toString()方法，然后将结果打印出来

输出重定向：

这意味着你程序运行的结果将会存放在result.txt中，此时在标准输出设备上将不会出现输出的结果

```java
System.err.println("路径:"+f.getPath());
System.err.println("大小:"+f.length()+" bytes" );
```

![image-20210714144629734](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714144629734.png)



#### 4. 文本文件的读写



**写文件：创建、写入数据、关闭**

用到三个类：

FileOutputStream  往文件写字节

OutputStreamWriter  字节和字符的转化

BufferedWriter 写缓冲区类，加速写操作 write() newline()

```java
FileOutputStream fos = null;
OutputStreamWriter osw = null;
BufferedWriter bw = null;
try {
    fos = new FileOutputStream("E:\\temp\\test.txt");
    osw = new OutputStreamWriter(fos,"UTF-8");
    bw = new BufferedWriter(osw);
    bw.write("我是");
    bw.newLine();
    bw.write("xxx");
    bw.newLine();
}catch(Exception e) {
    e.printStackTrace();
}finally {
    try {
        bw.close();
    }catch(Exception w) {
        w.printStackTrace();
    }
}
```

**读文件：打开，逐行读，关闭**

FileInputStream  往文件写字节

InputStreamReader  字节和字符的转化

BufferedReader 写缓冲区类 readLine()

```java
FileInputStream fis = null;
InputStreamReader isr = null;
BufferedReader br = null;
try {
    fis = new FileOutputStream("E:\\temp\\test.txt");
    isr = new OutputStreamWriter(fis,"UTF-8");
    br = new BufferedWriter(isr);
    String line;
    while((line=br.readLine())!=null){
        System.out.print(line);
    }
}catch(Exception e){
    e.printStackTrace();
}finally{
    try {
        br.close();
    }catch(Exception w) {
        w.printStackTrace();
    }
}
```

#### 4. 二进制文件的读写

写文件：

FileOutputStream

BufferedOutputStream

DataOutputStream：flush()，write()

```java
FileOutputStream fos = null;
BufferedOutputStream bos = null;
DataOutputStream dos = null;
try{
    fos = new FileOutputStream("E:\\temp\\test.txt");
    bos = new BufferedOutputStream(fos);
    dos = new DataOutputStream(bos);
    
    dos.writeUTF("a");
    dos.writeInt(20);
}catch(Exception e){
    e.printStackTrace();
}finally{
    try{
        dos.close();
    }catch(Exception e){
        e.printStackTrace();
    }
}
```

读文件：

FileInputStream

BufferedInputStream

DataInputStream：read()



#### 5. 用文本流读取和写入文件

读取Unicode信息的常用方法：BufferedReader

FileReader、FileWriter

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210714181632838.png" alt="image-20210714181632838" style="zoom:50%;" />

```java
class BufferedReaderDemo{
    public static void main(String args[]){
        try {
            FileReader fr = new FileReader("student.txt"); //源文件
            BufferedReader br = new BufferedReader(fr);
            while((read = br.readLine())!= null)
                System.out.println(read);
            fr.close();
            br.close();
        } catch (IOException ie){
            System.err.println(ie.getMessage());
        }
    }
}
```

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210924213859.png" alt="image-20210714182120477" style="zoom:50%;" />

![img](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210924215030.png)

![img](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210924222151.gif)

```java
//BufferedWriter的方法
void close() Close the stream.
void flush() Flush the stream.
void newLine () Write a line separator. //换行
void write (char[] cbuf, int off, int len) Write a portion of an array of characters.
void write(int c) Write a single character.
void write (String s, int off, int len) Write a portion of a String.
```
