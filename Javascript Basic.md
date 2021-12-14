## Javascript

caiyi 2021/7/30

### 一、初识JS

**解释型语言和编译型语言：**

程序语言翻译成机器语言，一种是编译，一种是解释

**编译器**在代码执行之前编译，生成中间代码文件

**解释器**是在运行是进行及时解释，并立即执行

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210802170554.png" alt="image-20210731102954630"  />

运行在客户端的脚本语言，不需要编译，运行过程中由js解释器逐行来进行解释并执行

现在也可以基于node.js技术进行服务器端的编程

- **作用**：表单动态校验，网页特效，服务端开发，桌面程序，app，物联网，游戏开发

- 浏览器执行JS简介：

  渲染引擎：解析HTML/CSS

  JS引擎：读取网页中的JS代码，对其处理后运行，chorme的V8，执行代码时逐行解释每一句源码

- **JS组成**：ECMAScript(语法)，DOM(页面文档对象模型)，BOM(浏览器对象模型)

  ECMAScript

- **三种写法**：

行内样式，可读性差在html中编写JS，不方便阅读

```html
<body>
    <input type="button" value="点我试试" onclick="alert('hello world')"/>
</body>
```

内嵌式，最常用的

```html
<script> alert('s沙漠');
</script>
```

外部JS文件，中间不可以写代码

```html
<script src='my.js'></script>
```

注意：JavaScript中都使用单引号

- **注释**  // (ctrl+/)  /**/  (shift+alt+A)
- **输入输出语句**

| 方法             | 说明               | 归属   |
| ---------------- | ------------------ | ------ |
| alert(msg)       | 浏览器弹出警示框   | 浏览器 |
| console.log(msg) | 控制台打印输出信息 | 浏览器 |
| prompt(info)     | 弹出输入框         | 浏览器 |

<u>注意：prompt取过来的值都是字符型的</u>

- **JS的变量**

  变量是在内存中用于存储数据的容器空间

  变量的初始化：1.声明 2. 赋值

```javascript
var age;
var urname = prompt('请输入姓名');
console.log(urname);
alert(urname);
```

声明变量的特殊情况

| 情况                         | 说明                                    | 结果      |
| ---------------------------- | --------------------------------------- | --------- |
| var age;  console.log(age);  | 只声明，不赋值                          | undefined |
| console.log(age);            | 不声明 不赋值 直接使用                  | 报错      |
| age = 10;  console.log(age); | 不声明 只赋值（不提倡，会变成全局变量） | 10        |

- **变量命名规范：**

  由字母/数字/下划线/美元符号组成

  严格区分大小写

  不能以数字开头，符号只能美元符号/下划线

  不能是关键字/保留字（var for）

  变量名必须见名知意/驼峰式命名

案例：交换两个变量的值

```javascript
var change1, change2 = 21, change3 = 34;
change1 = change2;
change2 = change3;
change3 = change1;
console.log(change2,change3);
```



### 二、数据类型

JavaScript是一种弱类型或者说动态语言，不用提前声明变量类型，在运行过程中自动确定

js拥有动态类型，变量的数据类型是可以变化的

**获取变量类型**

```javascript
var num = 10;
console.log(typeof num); //number
var timer = null;
console.log(typeof timer); //object
```

- **简单数据类型**（Number，Boolean，String，Undefined，Null）

  - number：八进制前加0，十六进制前加0x

    Number.MAX_VALUE

    Number.MIN_VALUE

    Infinity 无穷大

    NaN  isNaN() 判断是非数字

  - String：单引号

    长度计算 str.length()

    两个引号嵌套，外单内双或外双内单

    转义符\n \t \b

    字符串拼接用加号 'tianguan' + 'cifu'

    字符串 + 其他类型 = 字符串

  - Boolean

    true参与加法运算当1，false当0

    true +1 = 2

    flase + 1 = 1

  - undefined 未定义的数据类型

    一个声明后没有被赋值的变量会有一个默认值undefined

    var variable = undefined;

    variable + 'caiyi' = 'undefinedcaiyi'

    variable + 1 = NaN

  - Null

    var space = null;

    space + 'caiyi' = 'nullpink'

    space + 1 = 1

- **复杂数据类型**（object）

  

**数据类型转换：**

转换为字符型

```javascript
var num = 1;
str = num.toString();
str = String(num);
str = num + ''; //隐式转换
```

转换为整型

```javascript
var str = '530.9';
num = parseInt(str); //530, 只能得到整数，向下取整，不会四舍五入
num = ParseFloat(str); //得到浮点数
num = Number(str);
num = str - 0;// 用 - * / 做隐式转换
num = str * 1;

console.log(parseInt('3.94')); //3
console.log(parseInt('120px')); //120
console.log(parseInt('rem120px')); //NaN 
```

转化为布尔型

```javascript
Boolean(varb);

Boolean('');    //false
Boolean(0);     //false
Boolean(NaN);   //false
Boolean(null);  //false
Boolean(undefined);//false
//除了以上五种情况其他都是true
```

##### JS命名规范

标识符命名规范：变量、函数的命名必须要有意义，变量一般使用名词，函数一般使用动词

操作符命名规范：一般操作符前后都由空格

单行注释规范：单行注释前有个空格

其他规范：括号前后空格，花括号对齐



### 三、运算符

运算符operator也成为操作符

##### 1. 算数运算符 +-*/%

浮点数运算会出现误差，尽量不使用

```javascript
console.log(0.1 + 0.2) // 0.30000000000000004
console.log(0.07 * 100) //7.000000000001
console.log(num == 0.3) //false
```

##### 2. 递增递运算符

前置递增：先加一，后返回值

后置递增：先返回原值，后自加

```javascript
var num = 10;
++num + 10 //21
num++ + 10 //20

var e = 10;
var f = e++ + ++e; //22
```

##### 3. 比较运算符

< >  >= <=

= 赋值（把右边的值给左边）

== 默认转换数据类型（把字符串型数据转换为数字型）

===全等（值和数据类型一模一样）

```javascript
console.log(18 == ‘18’); //true
console.log(18 == ‘18’); //false
```

##### 4. 逻辑运算符

与&& 或|| 非!

逻辑与： 表达式1 && 表达式2 

两个都是 true 结果才是 true

逻辑或：表达式1 || 表达式2

两个都是 false 结果才是false



**逻辑中断（短路运算）**：

当多个表达式值可以确定结果时就不再继续运算右边表达式的值

运算符优先级

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20200314164506416.png" alt="pink-JSP54运算符优先级" style="zoom: 80%;" />



### 四、流程控制

![image-20210731120750599](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210731120750599.png)

#### 1. 顺序结构

按照代码先后顺序，依次执行

#### 2. 分支结构

if\if-else；如果if条件表达式结果为真，则执行大括号的代码

```javascript
if () {}
if () {
    ....
} else {
    ....
}
```

```html
//case 1
<input type="button" value="if语句案例" onclick="wangba()">
	<script>
		function wangba () {
			var wbage = prompt('how old r u');
			// if((Number(wbage)) >= 18){
			// 	alert('come in');
			// }
			if (wbage >= 18) {
				alert('come in');
			}
		}
	</script>
```

```html
//case 2 判断闰年
<input type="button" value="判断闰年" onclick="every4Year()">
	<script>
		function every4Year () {
			var urYear = prompt('年份');
			if(uryear % 4 == 0 && uryear % 100 != 0 || uryear % 400 == 0){
				alert('闰年');
			}else{
				alert('平年');
			}
		}
	</script>
```

三元表达式：

`条件表达式 ? 表达式1 : 表达式2 ;`

```javascript
var num = 10;
var result = num > 5 ? 'yes' : 'no';
console.log(result); //表达式是由返回值的
```

switch：

多分支语句 进行匹配 可以多选一

特定值比较合适，有范围的用 if else更合适

```javascript
switch(表达式){
	case value1: 执行语句; break;
	case value2: 执行语句;
	default: 执行语句;break；
```

```javascript
var melon = prompt('水果');
switch(melon){
		case 'apple': 
			alert('5.5yuan');
			break;
		case 'banana':
			alert('bananayuan');
			break;
		case '西瓜':
			alert('dont wanna melon');
			break;
		default:
			alert('nothing');
			break;
	}
```



#### 3. 循环结构

for循环：

```javascript
var sum = 0;
for(i=1;i<=100;i++){
    sum += i;
}
console.log(sum);
```

双重for循环：

```javascript
var star = '';
for(i=1; i<=10; i++){
    for(j=i; j<=10; j++){
        star += '⭐';
    }
    star += '\n';
}
console.log(star);
```

while循环：

```javascript
var doage = 1;
do{				
    console.log(doage);
    doage++;
}while(doage <= 10);
```

断点调试：在浏览器中F12进入开发者模式 -> source -> 找到文件 -> 单击行号打点 -> F11 下一步

continue：跳出本次循环，进入下一次循环

break：跳出整个循环



### 五、数组Array

在一个JavaScript数组，你可以放任意不同的数据类型

##### 创建数组

```javascript
var arr = new Array(); // 1.利用new创建空数组
var arry = [];  // 2.利用数组字面量

var arr = new Array(2); // 创建了长度为的为2的空数组
var arr = new Array('caiyi', 100); // 等价于 ['caiyi', 100] 表示2个数组元素
```

##### 遍历数组

```javascript
var arry = ['关羽','张飞','马超','赵云','黄忠','刘备','姜维'];
for (i = 0;i <= 6;i++) {
    console.log(arry[i]);
}
```

数组的长度（元素个数）：arr.length;

##### 新增元素

```javascript
// 1.修改length长度新增数组元素
var arr = [1, 2, 3];
arr.length = 5;
console.log(arr);    //[1,2,3,empty x 2]
console.log(arr[3]); //undefined
console.log(arr[4]); //undefined

// 2.修改数组索引新增元素
var arr = [1, 2, 3];
arr[0] = 0; // replace
arr[3] = 4; // append
console.log(arr);    //[0,2,3,4]
```

##### 筛选数组

可以用 newArr.length 作为插入的下标索引

```javascript
var arr1 = [2,0,6,1,77,0,52,0,25,7];
var newArr = [];
//刚开始 newArry.lengrh 就是0 
for (i = 0 ;i < arr1.length; i++) {
    if (arr1[i] >= 10) {
        newwArr[newArr.length] = arr1[i];
    }
}
```

##### 冒泡排序

```javascript
var arr1 = [5,4,3,2,1];
// 比较四趟
for (i = 0; i < arr1.length - 1; i++) {
    //每趟比较次数不同
    for (var j = 0; j < arr1.length - i - 1; j++) {
        // 每个数两两比较
        // if 里的 j 写成了 i ，出错 原因咦想通，花费30分钟
        if (arr1[j] > arr1[j + 1]) {
            var temp = arr1[j];
            arr1[j] = arr1[j + 1];
            arr1[j + 1] = temp;
        }
    }
}
console.log(arr1);
```



### 六、函数

##### 声明和调用函数

```javascript
// 1.利用函数关键字自定义函数（命名函数）
function fun () {
	......;
}
// 2.函数表达式（匿名函数）fun是变量名，不是函数名
var fun = function () {};

var fun = function (aru) {
    console.log('我是函数表达式');
    console.log(aru);
}
fun('pink老师');
```

##### 函数的参数

形参是接受实参的，类似于一个变量

```javascript
function cook(aru) { //形参
	console.log(aru);
}
cook('javascript');  //实参
```

| 参数个数         | **说明**                              |
| ---------------- | ------------------------------------- |
| 实参等于形参个数 | 输出正确结果                          |
| 实参多于形参个数 | 只取到形参的个数，多余的不要          |
| 实参小于形参个数 | 多的形参定义为 undefined ，结果为 NaN |

##### 函数返回值

函数只是实现某种功能，最终的结果需要返回给函数的调用

只要函数遇到 return 就把后面的结果返回给函数的调用者

```javascript
//求任意两数和
function getSum(num1, num2) {
    return num1 + num2;
}
console.log(getSum(1, 2));

//求数组中的最大值
function maxfun(arr) { //arr接受一个数组		
    var max = arr[0];
    for (i = 1;i < arr.length;i++) {
        if (max < arr[i]) {				
            max = arr[i];
        }
    }
    return max;			
}
//实参送一个数组过去
//用一个变量来接收 函数的返回结果 
var re = maxfun([5, 22, 99, 101, 67, 77]);
```

可使用数组返回多个值 return [num1 + num2, num1 - num2] 

函数都有返回值，有 return 则返回对应的值，否则返回 undefined

##### argument的使用

当不确定有多少个参数传递时可以使用 arguments 来获取，它是当前函数的一个**内置对象**。所有函数都内置了一个 arguments 对象，存储了所有实参

```javascript
function fun () {
    console.log(arguments); //[1,2,3]
    for (var i = 0; i < arguments.length; i++){
        console.log(argument[i]);
    }
}
fun(1,2,3);
```

arguments 是一个伪数组：

1. 具有数组的 length 属性
2. 按照索引的方式进行存储
3. 没有真正数组的一些方法 pop()，push() 等

利用函数求任意个数的最大值：

```javascript
function getMax () {
    var max = arguments[0];
    for (var i = 1; i < arguments.length; i++) {
        if (arguments[i] > max) {
            max = arguments[i];
        }
    }
    return max;
}
```



### 七、作用域

##### 定义

作用域：代码名字（变量）在某个范围内起作用和效果，目的是减少命名冲突

##### 作用域分类

es6之前分为两大类：**全局作用域**（整个script 标签或者一个单独的js文件），**局部作用域**（函数的内部）

**全局变量**在全局作用下使用，在局部变量内没有声明的变量也是全局变量

**局部变量**在局部作用下（在函数内部），只能在函数内部使用（函数的形参也是局部变量）

特殊情况：在函数内部，没有声明直接赋值的变量也属于全局变量

```javascript
function fun () {
    var num1 = 10;
    num2 = 20;
}
fun();
console.log(num1);//error
console.log(num2);//20
```

两个变量的区别：

全局变量只有在浏览器关闭时才会销毁，比较占内存资源

局部变量当程序执行完毕就会销毁，节约资源

扩展： js 在 es6 中新增块级作用域，花括号包裹即为**块级作用域**（{} if{} for{}）



##### 作用域链

内部函数访问外部函数表变量采取链式查找的方式，概括为**就近原则**

```javascript
var num = 10;
function fn () {
    var num = 20;
    function fun () {
        var num = 30;
    }
    function funct () {
        console.log(num); //30
    }
}
```



### 八、预解析

##### 案例引入

引入1

```javascript
console.log(num); //undefined
var num = 10;
```

引入2

```javascript
fn(); //11
function fn () {
    console.log(11);
}
```

引入3

```javascript
fun(); //error
var fun = function () {
    console.log(22);
}
```



##### 预解析的作用

JS代码是由浏览器中的JS解析器来执行的

JS 解析器在运行js代码时分为两步： 预解析和代码执行

**预解析**：js 引擎把 js 中所有的 var 和 function 提升到当前作用域的最前面

**代码执行**： 按照代码书写顺序从上往下执行

① 变量预解析（变量提升）：把所有变量==声明==提升到当前的作用域最前面，不提升赋值操作

```javascript
console.log(num); //undefined
var num = 10;
//预解析以后相当于执行了以下代码
var num;
console.log(num);
num = 10;
```

```javascript
fun(); // error
var fun = function() {
    console.log(22);
}
//预解析以后相当于执行了以下代码
var fun;
fun();
fun = function() {
    console.log(22);
}
```

② 函数预解析（函数提升）：把所有==函数声明==提升到当前作用域最前面 不提升函数

```javascript
fn(); //11
function fn () {
    console.log(11);
}
//预解析以后相当于执行了以下代码
function fn () {
    console.log(11);
}
fn(); //11
```



##### 预解析案例

```javascript
var num = 10;
fun();
function fun () {
    console.log(num); //undefined
    var num = 20;
}
//预解析以后相当于执行了以下代码
var num;
function fun () {
    var num;
    console.log(num); //undefined
    num = 20;
}
num = 10;
fun();
```

```javascript
f1();
console.log(c);
console.log(b);
console.log(a);
function f1() {
    var a = b = c = 9;
    //相当于 var a = 9; b = 9; c = 9;
    //b 和 c 直接赋值，没有 var声明，作全局变量
    //集体声明应用逗号隔开 var a = 9, b = 9, c = 9;
    console.log(a); // 9
    console.log(b); // 9
    console.log(c);	// 9			
}

//预解析以后相当于执行了以下代码
function f1() {
    var a;
    a = b = c = 9;
    console.log(a); // 9
    console.log(b); // 9
    console.log(c);	// 9			
}
f1();
console.log(c); //9
console.log(b); //9
console.log(a); //报错，因为b、c是全局变量，a是局部变量
```



### 九、对象

##### 定义

对象是一组无序的相关**属性和方法**的集合

所有事物都是对象，例如字符串、数值、数组、函数等

**属性** ：事物的特征，在对象中用属性来表示（常用名词）

**方法**： 事物的行为，在对象中用方法来表示（常用动词）



##### 创建对象的三种方式

1. 利用字面量 {}

```javascript
var obj = {}; // 创建了一个空的对象
var obj = {
    uname: 'zhangcaiyi',
    age: 18,
    sex: '女',
    sayHi: function () {
        console.log('Hi!');
    }
}
// 属性或方法采用键值对的形式 属性名: 值 
// 多个属性间用','隔开
// 方法':'后面跟的是一个匿名函数
```

2. 利用 new Object

```javascript
var obj = new Object(); // 创建了一个空对象
obj.uname = 'zhangcaiyi';
obj.age = 18;
obj.sex = '女';
obj.sayHi = function () {
    console.log('Hi');
}
// 利用等号 = 赋值的方法添加对象的属性和方法
// 每个属性和方法之间用';'结束
```

3. 利用构造函数

利用函数的方法，重复相同的代码，把对象中的**相同属性和方法**抽离出来封装

```javascript
function SuperStar (uname, age, sex) {
    this.name = uname;
    this.age = age;
    this.sex = sex;
    this.sing = function(song) {
        console.log(song);
    }
}
var gd = new SuperStar('GD', 30, 'man'); // 调用构造函数 返回的是一个对象
var jay = new SuperStar('Jay',40,'man');
console.log(typeof gd); //object
jay.sing('稻香');

// 构造函数名首字母要大写
// 构造函数不需要 return 就可以返回结果
// 调用构造函数必须使用 new
```

##### 使用对象

```javascript
console.log(obj.uname);
console.log(obj['uname']);
obj.sayHi();
```



##### 概念辨析

1. 变量/属性/方法/函数辨析：

   变量：单独声明并赋值，使用时直接写变量名

   属性：在对象里不需要声明 使用时必须是 ==对象.属性==

   函数：单独声明并且调用 ==函数名()== 单独存在

   方法：在对象里调用时 ==对象.方法==

2. 构造函数和对象辨析：

   构造函数：如Star()，抽象了对象的公共部分封装，封装到函数里面，泛指一大类（class）

   对象：如new Star()，特指一个具体的事物，利用构造函数创建对象的过程也称为**对象的实例化**



##### new关键字

new 在执行函数时会做四件事
- 在内存中创建一个新的空对象
- 让 this 指向这个对象
- 执行构造函数内的代码，给新对象添加属性和方法
- 返回这个新对象（所以构造函数里不需要 return）



##### 遍历对象 for in

```javascript
var obj = {
    name: 'dora',
    age: 18,
    sex: 'woman',
    fn: function (){}
}
// for (变量 in 对象)
for (var k in obj) {
    console.log(k);      // 输出得到属性名name, age, sex
    console.log(obj[k]); // obj[k] 得到属性值，k不加引号噢
    //按顺序依次输出：属性名和属性值
}
```



### 十、内置对象

js 中对象分为： 自定义对象、内置对象、浏览器对象

学会使用MDN查询文档：https://developer.mozilla.org/zh-CN/

##### MATH

不是一个构造函数，所以不需要 new 来调用，而是直接使用里面的方法和属性

```javascript
Math.PI 				// 圆周率
Math.floor()		    // 向下取整
Math.ceil()				// 向上取整
Math.round()			// 四舍五入版 就近取整  -3.5 结果为 -3
Math.abs()				// 绝对值
Math.max()	            // 最大值
Math.min()	            // 最小值
```

```javascript
//max方法说明
console.log(Math.PI);           //一个属性 圆周率
console.log(Math.max(1, 99,3)); // 99
console.log(Math.max(-1, -10)); // -1
console.log(Math.max(1, 99, 'pink')); // NaN 有字符串或其他类型数据
console.log(Math.max());              // -Infinity 空值返回负无穷
```

随机数方法random()

 Math.random() 返回一个 [0,1) 随机的小数

Math.getRandomInt() 返回一个 [min, max) 的随机整数

```javascript
function getRandomInt (min, max) {
    min = Math.ceil(min);
    max = Math.floor(max);
    return Math.floor( Math.random() * (max - min) ) + min;
}
```

Math.getRandomIntInclusive() 返回一个 [min, max] 的随机整数，包含 min 和 max

```javascript
function getRandomIntInclusive (min, max) {
    min = Math.ceil(min);
    max = Math.floor(max);
    return Math.floor( Math.random() * (max - min + 1) ) + min;
}
// 随机点名
var arr = ['张三', '张三丰', '李四', '李思思'];
console.log(arr[getRandomIntInclusive(0,3)]);
```



##### DATE

跟math不一样的是，date是一个**构造函数**，必须用new来调用创建日期对象

1. 使用 Date 如果**没有参数**，则返回当前系统的当前时间

```javascript
var date = new Date();
console.log(date); 
//Sun Aug 01 2021 17:10:18 GMT+0800 (中国标准时间)
```

2. 参数的常用写法：

   数字型 2020, 04, 05  数字用逗号隔开

   字符串型 '2020-04-05 16:34:59' 日期用横线隔开，时间用冒号隔开

```javascript
var date1 = new Date(2020, 4, 5);
console.log(date1); 
// Fri May 05 2020 00:00:00 GMT+0800 (中国标准时间)
// 注意：返回的是5月，而不是4月

var date2 = new Date('2020-04-05 16:34');
console.log(date2);
// Sun Apr 05 2020 16:34:00 GMT+0800 (中国标准时间)
```

3. 格式化日期：

| 日期格式化常用方法 | 含义                      | 代码              |
| ------------------ | ------------------------- | ----------------- |
| getFullYear()      | 获取当年                  | obj.getFullYear() |
| getMonth()         | 获取当月  0-11            | obj.getMonth()    |
| getDate()          | 获取当天日期              | obj.getDate()     |
| getDay()           | 获取星期几 （0-6）周日为0 | obj.getDay()      |
| getHours()         | 获取当前小时              | obj.getHours()    |
| getMinutes()       | 获取当前分钟              | obj.getMinutes()  |
| getSeconds()       | 获取当前秒钟              | obj.getSeconds()  |

函数使用的举例：

```javascript
var date3 = new Date();
console.log(date3.getFullYear()); // 返回当前日期的年 
console.log(date3.getMonth() + 1); // 月份 0-11
```

格式化时分秒的例子：

```javascript
function getTime() {
    var time = new Date();
    var h = time.getHours();
    h = h < 10 ? '0' + h : h;
    var m = time.getMinutes();
    m = m < 10 ? '0' + m : m;
    var s = time.getSeconds();
    s = s < 10 ? '0' + s : s;
    return h + ':' + m + ':' + s ;
}
console.log(getTime());
```

获取日期的总的毫秒数（时间戳）：

从1970年1月1日开始起到现在的毫秒数

```javascript
// 1. 通过 valueOf() getTime()
var date = new Date();
console.log(date.valueOf());
console.log(date.getTime());

// 2. 简单的写法 （最常用）
var date1 = +new Date(); // +new Date() 返回的就是总毫秒数
console.log(date1);

// 3. h5 新增的 获得总的毫秒数
console.log(Date.now());
```

4. 倒计时：

核心算法：输入时间减去现在的时间即倒计时，但不能拿时分秒相减，用时间戳来完成

把剩余时间转换为天，时，分，秒

公式如下：

```javascript
d = parseInt(总秒数/60/60/24);	// 计算天数
h = parseInt(总秒数/60/60%24); 	// 计算小时
m = parseInt(总秒数/60%60);        // 计算分数
s = parseInt(总秒数%60); 		   // 计算当前秒数
```

```javascript
// 下面转换时间
function countDown (time) {
    var nowTime = +new Date();       // 获取当前时间
    var inputTime = +new Date(time); // 获取输入的时间
    var times = (inputTime - nowTime) / 1000; // 剩余时间 秒数
    
    var d = parseInt(times/60/60/24);
    d = d < 10 ? '0' + d : d;
    var h = parseInt(times/60/60%24);
    h = h < 10 ? '0' + h : h;
    var m = parseInt(times/60%60);
    m = m < 10 ? '0' + m : m;
    var s = parseInt(times%60);
    s = s < 10 ? '0' + s : s;
    
    return d + '天' + h + '小时' + m + '分钟' + s + '秒' ;

}
console.log(countDown('2020-4-7 16:00:00'));
```



##### ARRAY

检测是否为数组的两种方式：

```javascript
// 1.instanceof
var arr = [];
consolo.log(arr instanceof Array); //true
var obj = {};
consolo.log(obj instanceof Array); //false

// 2.Array.isArray()
consolo.log(Array.isArray(arr));  //true
consolo.log(Array.isArray(obj));  //false
```

添加删除数组元素：

| 方法       | 说明                               | 返回值         |
| ---------- | ---------------------------------- | -------------- |
| push(x)    | 在数组末尾添加元素，修改i原数组    | 数组长度       |
| pop()      | 删除数组最后一个元素，把数组长度-1 | 删除的元素     |
| unshift(x) | 在数组开头添加元素，修改i原数组    | 数组长度       |
| shift()    | 删除数组的第一个元素               | 第一个元素的值 |

```javascript
var arr = [1, 2, 3];
arr.push(4,5); //[1,2,3,4,5]
console.log(arr.push(4,5,6)); //5
arr.unshift(0) //[0,1,2,3,4,5]
```

数组排序：

```javascript
arr.reverse();  //翻转数组
arr.sort();     //冒泡排序，把数字当成字符串排序，结果[1,13,4,7,77]
arr.sort(function(a,b) {
    return a-b; //升序排列 [1,4,7,13,77]
})
```

返回数组索引号：

| 方法名                    | 说明                         | 返回值          |
| ------------------------- | ---------------------------- | --------------- |
| arr.indexOf( ’blue‘ )     | 从前面开始查找到的第一个元素 | 不存在则返回 -1 |
| arr.lastIndexOf( ’blue‘ ) | 从后面开始查找               | 不存在则返回 -1 |

数组去重：

核心算法： 遍历旧数组，拿着旧数组去查询新数组，该元素没出现过则添加，否则不添加

利用 新数组.indexOf(数组元素) 返回 -1，则表示不重复

```javascript
function unique(arr) {
    var newArr = [];
    for (var i = 0; i < arr.length; i++) {
        if (newArr.indexOf(arr[i]) === -1) {
            newArr.push(arr[i]);
        }
    }
    return newArr; // 遍历完毕后返回
}
```

数组转换为字符串：

```javascript
arr.toString();
arr.join('分割符');

//example
var arr = [1,2,3];
console.log(arr.toString()); //1,2,3
var arr = ['green','pink','blue'];
console.log(arr.join('-')); //green-pink-blue
```

其他常用函数：

| 方法名   | 作用                                     | 返回值                               |
| -------- | ---------------------------------------- | ------------------------------------ |
| concat() | 连接两个或多个数组 不影响原数组          | 返回新数组                           |
| slice()  | 数组截取slice(begin, end)                | 返回被截取项目的新数组               |
| splice() | 数组删除splice(第几个开始，要删除的个数) | 返回被删除项目的新数组，会影响原数组 |

```javascript
var uniq1 = [1, 2, 3, 4, 5];
var uniq2 = [6, 7, 8, 9, 0];
var uniq3 = [];
var uniq4 = [6, 7, 8, 9, 0];
console.log(uniq3.concat(uniq1, uniq2)); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]
console.log(uniq1.slice(1,3)); // [2,3] 默认不包括结束位置的元素
console.log(uniq1); // 不变 [1, 2, 3, 4, 5]
console.log('uniq4+' + uniq4); // uniq4+6,7,8,9,0
console.log(uniq4.splice(2,2)); //[8, 9]
console.log('splice后的' + uniq4); // splice后的6,7,0
```



##### STRING

**基本包装类型**：把简单数据类型包装成为复杂数据类型，这样基本数据类型就有了属性和方法

js 提供了三种基本包装类型：String，Number，Boolean

```javascript
var str = ‘uniq’;
console.log(str.length); // 基本数据类型本无属性和方法
//但以上代码可执行是因为 JS 会把基本数据类型包装为复杂数据类型 执行过程如下：

// 1. 生成临时变量，把简单数据类型包装为复杂数据类型
var temp = new String(‘uniq’);
// 2. 赋值给我们声明的字符变量
str = temp;
// 3.销毁临时变量
temp = null;
```

**字符串的不可变性**：

指的是里面的值不变，实质改变的是地址 在内存中开辟了新的存储空间（指针改变了）

![image-20210802134137579](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210802170748.png)

- 当重新给 str 赋值时， 常量 ‘andy’ 不会被修改，但依然在内存中
- 重新给字符串赋值，会重新在内存中开辟空间 'red' ，这就是字符串的不可变
- 由于字符串的不可变，在大量拼接字符串时就会产生效率问题

**返回字符的位置：**

```javascript
str.indexOf(x,a,b); //从a的索引号开始查找x，到b（不包括）
str.lastIndexOf(x);
```

例子：查找 ’abcosidfnoiojisoo' 中所有o出现的位置以及次数

```javascript
var str = ’abcosidfnoiojisoo',
var index = str.indexOf('o');
var num = 0;
while(index !== -1) {
    console.log(index);
    num++;
    index = str.indexOf('red', index + 1);
}
```

**根据索引号返回字符**：

| 方法名                | 作用                                            |
| --------------------- | ----------------------------------------------- |
| str.charAt(index)     | 返回指定位置的字符（index字符串的索引号）       |
| str.charCodeAt(index) | 获取指定位置处字符的ASCII码，判断用户按了哪个键 |
| str[index]            | 获取指定位置处字符，h5, IE8+支持                |

例子：统计出现最多的字符和次数

核心算法：利用 charAt() 遍历这个字符串

把每个字符都存储给对象，若没有该属性就为 1，若存在了就 +1

```javascript
var str = 'abcoefoxyozz';
var obj = {};
for (var i = 0; i < str.length; i++) {
    var chars = str.charAt(i); //chars 是字符串的每一个字符
    if (obj[chars]) {
        obj[chars]++;  // 属性存在则加一
    } else {
        obj[chars] = 1;
    }
}

var max = 0;
var ch = '';
for (var k in obj) {
    if (obj[k] > max) { // k是属性名
        max = obj[k]; // obj[k] 是属性值
        ch = k;
    }
}
```

**字符串操作方法**：

| 方法                        | 说明                                             |
| --------------------------- | ------------------------------------------------ |
| str.concat(str1,str2,str3…) | 连接两个字符串，等效于 +                         |
| str.substr(start,length)    | (start索引号, length取的个数)                    |
| str.replace(x, y)           | (‘被替换的字符’, ‘替换为的字符’)  只会替换第一个 |
| str.slice(start,end)        | 删除子字符串，(开始位置, 结束位置) end取不到     |
| str.substring(start, end)   | 基本与 slice 相同，但不取负值                    |
| str.split('分隔符')         | join 把数组转换为字符串，split把字符串转化为数组 |
| str.toUpperCase()           | 全部转换大写                                     |
| str.toLowerCase()           | 全部转换小写                                     |

``` javascript
//把所有o都替换为i
var str = 'ooooooooo';
while (str.indexOf('o') != -1) {
    str.replace('o','i');
}
//分隔符举例
var str = 'green-red-pink-blue';
console.log(str.split('-')); //[green,red,pink,blue]
```



##### 简单数据类型和赋值数据类型

简单类型又叫做基本数据类型或者 **值类型**：在存储中就是值的本身

string, number, boolean, undefined, null

复杂类型又叫做 **引用类型**：在存储时变量中存储的仅仅是地址（引用）

通过 new 关键字创建的对象（系统对象、自定义对象），如 Object、Array、Date等



栈（操作系统）：由操作系统自动分配释放存放函数得参数值、局部变量得值等，**简单数据类型存放到栈里面**

堆（操作系统）：存储复杂类型（对象），一般由程序员分配释放，若程序员不释放，由垃圾回收机制回收，**复杂数据类型存放到堆里面**



简单数据类型传参：函数的形参可以看作一个变量，当我们把一个值类型作为参数传给函数得形参时，其实是把变量在栈空间里得值**复制了一份给形参**，在方法内部对形参做任何修改都不会影响到外部变量

复杂数据类型传参：函数得形参也可以看作是一个变量，当我们把引用类型变量传给形参时，其实是把变量在栈空间里保存得地址复制给了形参，**实参和形参保留得是同一个堆地址**，所以操作的是同一个对象

```javascript
function Person(name) {
    this.name = name;
}
function f1(x) {
    console.log(x.name); // 2. 刘德华
    x.name = '张学友';
    console.log(x.name); // 3. 张学友
}
var p = new Person('刘德华');
console.log(p.name); // 1. 刘德华
f1(p);
console.log(p.name); // 4.张学友
```

