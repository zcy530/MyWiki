

# JavaScript进阶 | DOM

caiyi 2021/8/2



## 一、DOM简介

文档对象模型（Document Object Model，简称 DOM），是 W3C 组织推荐的处理可扩展标记语言（HTML或者XML）的标准编程接口

W3C 已经定义了一系列的 DOM 接口，通过这些 DOM 接口可以改变网页的**内容、结构和样式**。

**dom树**：

![image-20210803151805136](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210804172754.png)

文档：一个页面就是一个文档，DOM中使用doucument来表示

元素：页面中的所有标签都是元素，DOM中使用 element 表示

节点：网页中的所有内容都是节点（标签，属性，文本，注释等），DOM中使用node表示

DOM 把以上内容都看做是对象



## 二、获取元素

### 1. 根据ID获取

可以获取带ID的元素对象

```javascript
doucument.getElementByld('id名')
// 参数id是大小写敏感的字符串，所以 time 一定要加引号
// 返回的是一个元素对象不是字符串
```

```html
<div id="time">2021-8-3</div>
<script>
    // 因为我们文档页面从上往下加载，所以得先有标签，所以script写在标签下面
    var timer = document.getElementById('time');
    console.log(timer); //<div id="time">2021-8-3</div>
    console.dir(timer); // 打印元素对象的属性和方法 //dic#time
</script>
```

### 2. 根据标签名获取

根据标签名获取，返回带有指定标签名的对象的集合

```javascript
doucument.getElementsByTagName('标签名');
// 返回的是获取过来元素对象的集合 以伪数组的形式存储
```

```html
<ul>
    <li>知否知否</li>
    <li>知否知否</li>
    <li>知否知否</li>
</ul>
<script>
    var lis = document.getElementsByTagName('li');
    console.log(lis);  //HTMLcollection(3) [li,li,li]
    console.log(lis[0]); //<li>知否知否</li>
    // 依次打印,遍历
    for (var i = 0; i < lis.length; i++) {
        console.log(lis[i]);
    }
    // 如果页面中只有 1 个 li，返回的还是伪数组的形式
    // 如果页面中没有这个元素，返回的是空伪数组
</script>
```

### 3. 根据父元素+标签名获取

还可以根据标签名获取某个元素（父元素）内部所有指定标签名的子元素,获取的时候不包括父元素自己

```javascript
element.getElementsByTagName('标签名')
ol.getElementsByTagName('li');
```

```html
<script>
    //element.getElementsByTagName('标签名'); 父元素必须是指定的单个元素
    var ol = document.getElementById('ol');
    console.log(ol[0].getElementsByTagName('li'));
</script>
```

注意：父元素必须是单个对象(必须指明是哪一个元素对象)，不能是伪数组，会报错

### 4. 通过H5新增方法获取

注意html5是ie9以上的版本才支持的

- 根据类名return元素对象合集伪数组

```javascript
document.getElementsByClassName('类名'); 
```

- 根据指定选择器（.类选择器，#id选择器，标签选择器）return第一个元素对象

```javascript
document.querySelector('选择器');
```

- 根据指定选择器（.类选择器，#id选择器，标签选择器）retrun所有元素对象合集，伪数组

```javascript
document.querySelectorAll('选择器');
```

用法举例：

```html
<div class="box"></div>
<div class="box"></div>
<div id="nav">
    <ul>
        <li>首页</li>
        <li>产品</li>
    </ul>
</div>
<script>
    var boxs = document.getElementsByClassName('box'); 
	console.log(boxs); //HTMLcollection(2) [div.box,div.box]
    
    var firstBox = document.querySelector('.box');
    console.log(firstBox); //<div class="box"></div>
    
    var nav = document.querySelector('#nav');
    console.log(nav);
    
    var li = document.querySelector('li');
    console.log(li); //<li>首页</li>
    
    var allBox = document.querySelectorAll('.box');
    console.log(allBox); //HTMLcollection(2) [div.box,div.box]
    
    var lis = document.querySelectorAll('li');
    console.log(lis);
</script>
```

### 5. 获取body和html元素对象

```javascript
document.body; //返回body元素对象
document.documentElement; //返回html元素对象
```



## 三、事件基础

JavaScript 使我们有能力创建动态页面，而事件是可以被 JavaScript 侦测到的行为。

### 1. 事件三要素

事件源：事件被触发的对象

事件类型：如何触发，什么事件，比如是鼠标点击，还是鼠标经过，还是键盘按下

事件处理程序：通过一个函数赋值的方式完成

```html
<script>
    var btn = document.getElementById('btn');
    btn.onclick = function() {
        alert('吃麻辣鸡');
    }
</script>
```

### 2. 执行事件的步骤

1. 获取事件源
2. 注册事件(绑定事件)
3. 添加事件处理程序(采取函数赋值形式)

```html
<div>1234</div>
<script>
    var div = document.querySelector('div');
    div.onclick = function() {
        console.log('我被选中了');
    }
</script>
```

鼠标事件类型：

| 鼠标事件    | 触发条件         |
| ----------- | ---------------- |
| onclick     | 鼠标点击左键触发 |
| onmouseover | 鼠标经过触发     |
| onmouseout  | 鼠标离开触发     |
| onfocus     | 获得鼠标焦点触发 |
| onblur      | 失去鼠标焦点触发 |
| onmousemove | 鼠标移动触发     |
| onmouseup   | 鼠标弹起触发     |
| onmousedown | 鼠标按下触发     |



## 四、操作元素

JavaScript 的 DOM 操作可以改变网页内容、结构和样式，我们可以利用 DOM 操作元素来改变元素里面的内容 、属性等。注意以下都是属性

### 1. 改变元素的内容

从起始位置到终止位置的内容，不识别html标签，去除空格和换行，非标准

```
element.innerText = 'str'
```

起始位置到终止位置的全部内容，识别HTML标签，保留空格和换行，W3C标准

```
element.innerHTML
```

这两个属性都是可读写的  可以获取元素里面的内容

innerText 和 innerHTML 只能修改普通盒子，比如div标签里面的内容

```html
<div></div>
<p>
    我是文字
    <span>123</span>
</p>

<script>
    var div = document.querySelector('div');
    div.innerText = '<strong>今天是：2021</strong>'; //不会加粗
    div.innerHTML = '<strong>今天是：2021</strong>'; //会加粗

    var p = document.querySelector('p');
    console.log(p.innerText);
    console.log(p.innerHTML);
</script>
```

![image-20210804095354780](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210804095634.png)



### 2. 改变元素属性

修改img属性：

```javascript
img.src = 'xxx';
img.title = 'xxx';
```

通过点击不同按钮切换图片举例：

```html
<button id="ldh">刘德华</button>
<button id="zxy">张学友</button>
<img src="images/ldh.jpg" title="刘德华">

<script>
    var ldh = document.getElementById('ldh');
    var zxy = document.getElementById('zxy');
    var img = document.querySelector('img');

    zxy.onclick = function() {
        img.src = 'images/zxy.jpg';
    }
    ldh.onclick = function() {
        img.src = 'images/ldh.jpg';
    }
</script>
```



修改表单属性：

```javascript
input.value = 'xxx';
input.type = 'xxx';
input.checked = 'xxx';
input.selected = true / false;
input.disabled = true / false;  //禁用了
```

```javascript
btn.onClick = function() {
	input.value = 'clicked';
    this.disabled = true; //this指向的是函数事件的调用者
}
```



### 3. 改变样式属性

我们可以通过 JS 修改元素的大小、颜色、位置等样式

```javascript
// 行内样式操作 element.style
div.style.backgroundColor = 'pink';
div.style.width = '250px';
box.style.display = 'none';
// 类名样式操作 element.className 
```

两种操作方法改变样式属性对比举例：

```html
<sytle>
    .change {
    	background-color: purple;
    	color: #fff;
    	font-size: 25px;
    }
</sytle>

<div class="first">文本</div>
<script>
    var test = document.querySelector('div');
    test.onclick = function() {
        // 1. 使用 element.style 获得修改元素样式，样式比较少或者功能简单的情况下
        this.style.backgroundColor = 'purple';
        this.style.color = '#fff';
        this.style.fontSize = '25px';

        // 2. 通过 element.className 更改元素的样式，适合于样式较多或者功能复杂的情况
        this.className = 'change';
        
        // 3. 如果想要保留原先的类名，我们可以这么做：多类名选择器，两个类名用空格隔开
        this.className = 'first change';
    }
</script>
```

注意：

- JS里面的样式采取驼峰命名法，比如 fontSize ，backgroundColor
- JS 修改 style 样式操作 ，产生的是 <u>行内样式</u>，CSS权重比较高
- 如果样式修改较多，可以采取操作类名方式更改元素样式
- class 因为是个保留字，因此使用 <u>className</u> 来操作元素类名属性
- className 会直接更改元素的类名，会覆盖原先的类名



### 4. 小总结

![image-20210804114054513](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210804114056.png)



### 5. 排他思想

如果有同一组元素，我们想要某一个元素实现某种样式，需要用到循环的排他思想算法

首先先排除其他人，然后才设置自己的样式 这种排除其他人的思想我们成为排他思想



![在这里插入图片描述](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210804114354.gif)

实现：

```html
<body>
    <button>按钮1</button>
    <button>按钮2</button>
    <button>按钮3</button>
    <button>按钮4</button>
    <button>按钮5</button>
    <script>
        // 1. 获取所有按钮元素
        var btns = document.getElementsByTagName('button');
        for (var i = 0; i < btns.length; i++) {
            btns[i].onclick = function() {
                // (1) 我们先把所有的按钮背景颜色去掉
                for (var i = 0; i < btns.length; i++) {
                    btns[i].style.backgroundColor = '';
                }
                // (2) 然后才让当前的元素背景颜色为pink
                this.style.backgroundColor = 'pink';
            }
        }
    </script>
</body>
```



### 6. 自定义属性

- 获取属性值

  ```javascript
  element.属性; //获取内置属性值 id className
  element.getAttribute('属性'); //获取自定义的属性 
  ```

- 设置属性值

  ```javascript
  element.属性 = '值';  //设置内置属性值 id class
  element.setAttribute('属性','值'); //设置自定义的属性
  ```

- 移除属性

  ```javascript
  element.removeAttribute('属性');
  ```

  

```html
<body>
    <div id="demo" index="1" class="nav"></div>
    <script>
        var div = document.querySelector('div');
        // 1. 获取元素的属性值
        console.log(div.id);
        console.log(div.getAttribute('id'));
        console.log(div.getAttribute('index'));
        
        // 2. 设置元素属性值
        div.id = 'test';
        div.className = 'navs';
        
        div.setAttribute('index', 2);
        div.setAttribute('class', 'footer'); // 这里面写的就是class 不是className
        
        // 3 移除属性 removeAttribute(属性)    
        div.removeAttribute('index');
    </script>
</body>
```



### 7. H5自定义属性

自定义属性目的：保存并保存数据，有些数据可以保存到页面中而不用保存到数据库中

有些自定义属性很容易引起歧义，不容易判断到底是内置属性还是自定义的，所以H5有了规定

- 设置H5自定义属性

  H5规定自定义属性 ==data-开头== 作为属性名并赋值

  ```html
  <div data-index = "1"></>
  div.setAttribute('data-index',1);
  ```

- 获取H5自定义属性

  ```javascript
  element.getAttribute('data-index') //兼容性获取 
  element.dataset.index //H5新增的,IE11才开始支持
  element.dataset['index']
  ```

综合举例：

```html
<body>
    <div data-index="2" data-list-name="andy"></div>
    <script>
        var div = document.querySelector('div');
        
        div.setAttribute('data-time', 20);
        console.log(div.getAttribute('data-index'));
        console.log(div.getAttribute('data-list-name'));
        
        // dataset 是一个集合里面存放了所有以data开头的自定义属性
        console.log(div.dataset);
        console.log(div.dataset.index);
        console.log(div.dataset['index']);
        
        // 如果自定义属性里面有多个-链接的单词，我们获取的时候采取 驼峰命名法
        console.log(div.dataset.listName);
        console.log(div.dataset['listName']);
    </script>
</body>
```



### 8. 案例

- 仿京东显示隐藏密码明文案例 P17

- 仿淘宝关闭二维码 P20
- 循环精灵图 P21
- 显示隐藏文本框内容 P22
- 密码验证信息 P24
- 百度换肤效果 P27
- 表格隔行变色 P28
- 表单全选取消全选 P29
- tab栏切换 P33



## 五、节点操作

获取元素通常使用两种方式：

| **1.利用DOM提供的方法获取元素** | **2.利用节点层级关系获取元素** |
| ------------------------------- | ------------------------------ |
| document.getElementById()       | 利用父子兄节点关系获取元素     |
| document.getElementsByTagName() | 逻辑性强，但是兼容性较差       |
| document.querySelector()        |                                |
| 逻辑性不强，繁琐                |                                |

这两种方式都可以获取元素节点，我们后面都会使用，但是节点操作更简单

### 1. 节点概述

网页中的所有内容都是节点（元素、属性、文本等），在DOM 中，节点使用 node 来表示

HTML DOM 树中的所有节点均可通过 JavaScript 进行访问，均可被修改，也可以创建或删除。

节点至少有三个基本属性：

```
- node.nodeType（元素为nodeType1、属性为2、文本为3）
- node.nodeName
- node.nodeValue
```

我们在实际开发中，节点操作主要操作的是**元素节点**

利用 DOM 树可以把节点划分为不同的层级关系，常见的是**父子兄层级关系**

![image-20210803151805136](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210804144810.png)

### 2. 父级节点

```
node.parentNode
```

返回某节点最近的一个父结点

如果指定的节点没有父结点则返回null

```html
<div class="box">
    <span class="son">×</span>
</div>

<script>
    var child = document.querySelector('.son');
    console.log(child.parentNode);
</script>
```



### 3. 子结点

**获取所有子节点**

```javascript
Node.childNodes //标准
Node.children   //非标准
```

关于 Node.childNodes 的说明：

- Node.childNodes  返回包含指定节点的子节点的集合，即时更新

- 返回值包含了所有的子结点，包括元素节点，文本节点等
- 如果只想要获得里面的元素节点，则需要判断nodeType，所以一般不提倡使用 childNodes

关于 Node.children 的说明：

- `parentNode.children` 是一个只读属性，返回所有的子元素节点
- 它只返回子元素节点，其余节点不返回 （**这个是我们重点掌握的**）
- 虽然 children 是一个非标准，但是得到了各个浏览器的支持，因此我们可以放心使用

```javascript
var ul = document.querySelector('ul');
console.log(ul.childNodes);  // NodeList(9)
console.log(ul.children);    // HTMLCollection(4)
```



**第一个和最后一个子节点：**

```javascript
Node.firstChild      //返回第一个子节点，找不到则返回null
Node.lastChild       //返回最后一个子节点，找不到则返回null
Node.firstElementChild //返回第一个 **子元素节点** ，找不到则返回null
Node.lastElementChild  //返回最后一个 **子元素节点** ，找不到则返回null
// 后两种方法有兼容性问题，IE9以上才支持
```



**解决方案：**

firstChild 和 lastChild 包含其他节点，操作不方便，而 firstElementChild 和 lastElementChild 又有兼容性问题，那么我们如何获取第一个子元素节点或最后一个子元素节点呢？

```javascript
Node.chilren[0]  //返回第一个子元素节点
Node.chilren[Node.chilren.length - 1] //返回最后一个子元素节点
```

**案例：下拉菜单 P41**



### 4. 兄弟节点

**获取兄弟节点**

```javascript
node.nextSibling        //返回下一个兄弟节点
node.previousSibling    //返回上一个兄弟节点
node.nextElementSibling //返回下一个兄弟 **元素节点**
node.previousElementSibling  //返回上一个兄弟 **元素节点**
// 后两种方法有兼容性问题，IE9以上才支持
```

举例：

```html
<body>
    <div>我是div</div>
    <span>我是span</span>
    <script>
        var div = document.querySelector('div');

        console.log(div.nextSibling);		// #text
        console.log(div.previousSibling);	// #text

        console.log(div.nextElementSibling);	// <span>我是span</span>
        console.log(div.previousElementSibling);// null
    </script>
</body>
```



**解决方案：自己封装一个兼容性的函数**

```javascript
function getNextElementSibling(element) {
    var el = element;
    while(el = el.nextSibling) {
        if(el.nodeType === 1){
            return el;
        }
    }
    return null;
}
```



### 5. 创建节点

```javascript
var newNode = document.createElement('tagName');
```

**添加节点**

```javascript
node.appendChild(newNode)  // 后面追加元素
node.insertBefore(newNode,指定元素) //指定元素前面插入
```

我们想要页面添加一个新的元素分两步: 1. 创建元素 2. 添加元素

```html
<body>
    <ul>
        <li>123</li>
    </ul>
    <script>
        var ul = document.querySelector('ul');
        var li = document.createElement('li');
        ul.appendChild(li);

        var lili = document.createElement('li');
        ul.insertBefore(lili, ul.children[0]);
    </script>
</body>
```

**删除节点**

```javascript
node.removeChild(child) //从 DOM 中删除一个子节点，返回删除的节点
```

**复制节点**

```javascript
node.cloneNode()  
```

- node.cloneNode() 方法返回调用该方法的节点的一个副本。 也称为克隆节点/拷贝节点

- 括号参数为空或者为 false ，是**浅拷贝**，只复制节点本身，不复制里面的子节点

- 括号参数为 true ，是**深拷贝**，会复制节点本身，以及里面所有的子节点

  

**案例：简单版发布留言 删除留言 P44** 

```html
<textarea name="" id="">123</textarea>
<button>submit</button>
<ul></ul>
<script>
    //获取元素
    var btn = document.querySelector("button");
    var text = document.querySelector("textarea");
    var ul = document.querySelector("ul");
    //注册事件
    btn.onclick = function fun() {
        if (text.value == "") {
            alert("none");
        } else {
            // create element
            var newli = document.createElement("li");
            // append element
            ul.appendChild(newli);
            newli.innerHTML = text.value + "  <a href='javascript::'>delete</a>";
            // delete element
            var as = document.querySelectorAll("a");
            for (var i = 0; i < as.length; i++) {
                as[i].onclick = function fun() {
                    ul.removeChild(this.parentNode);
                };
            }
        }
    };
</script>
```

**案例：动态生成表格 P48**



### 6. 了解

**三种动态创建元素的方法**：

```javascript
- doucument.write()
- element.innerHTML
- document.createElement()
```

doucument.write 和 innerHTML 的区别：

- `document.write()` 是直接将内容写入页面的内容流，但是文档流执行完毕，则它会导致页面全部重绘
- `innerHTML` 是将内容写入某个 DOM 节点，不会导致页面全部重绘

createElement 和 innerHTML 区别：

- `innerHTML` 创建多个元素效率更高（不要拼接字符串，采取数组形式拼接），结构稍微复杂
- `createElement()` 创建多个元素效率稍低一点点，但是结构更清晰
- 总结：不同浏览器下， innerHTML 只要采取数组形式，效率都要比 createElement 高



**经典面试题**：

createElement 和 innerHTML 哪个创建元素的效率更高？👆



## 六、DOM 核心（半期总结）

对于DOM操作，我们主要针对子元素的操作，主要有

创建、增、删、改、查、属性操作、时间操作

### 1. 创建

1. document.write
2. innerHTML
3. createElement

### 2. 增加

1. appendChild
2. insertBefore

### 3. 删除

1. removeChild

### 4. 修改

主要修改dom的元素属性，dom元素的内容、属性、表单的值等

1. 修改元素属性：src、href、title 等
2. 修改普通元素内容：innerHTML、innerText
3. 修改表单元素：value、type、disabled
4. 修改元素样式：style、className

### 5. 查找

主要获取查询dom的元素

1. DOM提供的API方法：getElementById、getElementsByTagName
2. H5提供的新方法：querySelector、querySelectorAll (提倡)
3. 利用节点操作获取元素：parentNode、children、previousElementSibling、nextElementSibling

### 6. 属性操作

主要针对于自定义属性

1. setAttribute：设置dom的属性值
2. getAttribute：得到dom的属性值
3. removeAttribute：移除属性



## 七、事件高级 

### 1. 注册事件(绑定事件)

注册事件有两种方式：传统方式和方法监听注册方式

**(1) 传统方式：**

利用on开头的事件 ，特点是注册事件的唯一性，同一个元素同一个事件只能设置一个处理函数，最后注册的处理函数将会覆盖前面注册的处理函数

```
btn.onclick = function() {}
```

**(2) 方法监听注册方式：**

w3c 标准推荐方式，IE9 之前的 IE 不支持此方法，可使用 attachEvent() 代替

同一个元素同一个事件 ==可以注册多个监听器==，按注册顺序依次执行



```javascript
eventTarget.addEventListener(type,listener[,useCapture]) 
```

`type`: 事件类型字符串，click,mouseover，这里不要带on

`listener`：事件处理函数，事件发生时，会调用该监听函数

`useCapture`：可选参数，是一个布尔值，默认是 false



```
eventTarget.attachEvent(eventNameWithOn,callback)
```

`eventNameWithOn`：事件类型字符串，比如 onclick 、onmouseover ，这里要带 on

`callback`： 事件处理函数，当目标触发事件时回调函数被调用



```html
<button>传统注册事件</button>
<button>方法监听注册事件</button>
<button>ie9 attachEvent</button>
<script>
    var btns = document.querySelectorAll('button');
    // 1. 传统方式注册事件
    btns[0].onclick = function() {
        alert('hi');
    }
    // 2. 事件监听注册事件 addEventListener 
    btns[1].addEventListener('click', function() {
        alert(22);
    })
    // 3. attachEvent ie9以前的版本支持
    btns[2].attachEvent('onclick', function() {
        alert(11);
    })
</script>
```

**(3)注册事件兼容性解决方案**：

首先照顾大多数浏览器，再处理特殊浏览器

```javascript
 function addEventListener(element, eventName, fn) {
      // 判断当前浏览器是否支持 addEventListener 方法
      if (element.addEventListener) {
        element.addEventListener(eventName, fn);
      } else if (element.attachEvent) {
        element.attachEvent('on' + eventName, fn);
      } else {
        // 相当于 element.onclick = fn;
        element['on' + eventName] = fn;
 } 
```



### 2. 删除事件(解绑事件)

**(1) 传统方式删除事件**

```javascript
eventTarget.onclick = null;
```



**(2) 方法监听注册方式**

```
eventTarget.removeEventListener(type,listener[,useCapture]);
```

`type`：事件类型字符串，比如 click, mouseon, 不要带on

`listener`：注意这里不能用匿名函数的方法，调用不需要加小括号

`useCapture`：可选参数，是一个布尔值，默认是 false



```
eventTarget.detachEvent(eventNameWithOn,callback);
```

`eventNameWithOn`：事件类型字符串，比如 onclick, onmouseover，要带 on

`callback`： 不能用匿名函数的方法，调用不需要加小括号



**(2) 删除事件兼容性解决方案**

```javascript
 function removeEventListener(element, eventName, fn) {
      // 判断当前浏览器是否支持 removeEventListener 方法
      if (element.removeEventListener) {
        element.removeEventListener(eventName, fn);  // 第三个参数 默认是false
      } else if (element.detachEvent) {
        element.detachEvent('on' + eventName, fn);
      } else {
        element['on' + eventName] = null;
 } 
```



举例：点击一次就不再弹出对话框的实现

```html
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <script>
        var divs = document.querySelectorAll('div');
        // 1. 传统方式删除事件
        divs[0].onclick = function() {
            alert(11);
            divs[0].onclick = null;
        }
        // 2.removeEventListener 删除事件
        divs[1].addEventListener('click',fn);   //里面的fn不需要调用加小括号

        function fn(){
            alert(22);
            divs[1].removeEventListener('click',fn);
        }
        
        // 3.IE9 中的删除事件方式
        divs[2].attachEvent('onclick',fn1);
        function fn1() {
            alert(33);
            divs[2].detachEvent('onclick',fn1);
        }
    </script>
```



### 3. DOM事件流

事件流描述的是从页面中接收事件的顺序

事件发生时会在元素节点之间按照特定的顺序传播，这个**传播过程**即DOM事件流

![image-20210805172428904](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210805172431.png)

dom事件流分成三个阶段：

1. 事件捕获： 网景最早提出，由 DOM 最顶层节点开始，然后逐级向下传播到到最具体的元素接收
2. 当前目标阶段
3. 事件冒泡： IE 最早提出，事件开始时由最具体的元素接收，然后逐级向上传播到到 DOM 最顶层节点



注意：

1. JS 代码中只能执行捕获或者冒泡其中的一个阶段

2. onclick 和 attachEvent 只能得到冒泡阶段

3. 如果 addEventListener 第三个参数是 true 那么则处于捕获阶段，false 处于冒泡阶段

4. 有些事件是没有冒泡的，比如 onblur、onfocus、onmouseenter、onmouseleave

   

- **捕获阶段**

  document -> html -> body -> father -> son

  ```html
  <div class="father">
      <div class="son">son盒子</div>
  </div>
  <script>
      var son = document.querySelector('.son');
      son.addEventListener('click', function() {
          alert('son');
      }, true);
      var father = document.querySelector('.father');
      father.addEventListener('click', function() {
          alert('father');
      }, true);
  </script>
  ```

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/65d6a7c8038f414fbf03c3ac4d2ce293.gif#pic_center)

  

- **冒泡阶段**

  son -> father ->body -> html -> document

  ```html
  <div class="father">
      <div class="son">son盒子</div>
  </div>
  <script>
      var son = document.querySelector('.son');
      son.addEventListener('click', function() {
          alert('son');
      }, false);
      var father = document.querySelector('.father');
      father.addEventListener('click', function() {
          alert('father');
      }, false);
      document.addEventListener('click', function() {
          alert('document');
      })
  </script>
  ```

  ![在这里插入图片描述](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210808112239.gif)

  





### 4. 事件对象

event 对象代表事件的状态，比如键盘按键的状态、鼠标的位置、鼠标按钮的状态

事件对象只有有了事件才会存在，它是系统给我们自动创建的，不需要我们传递参数

```javascript
eventTarget.onclick = function(event) {
   // 这个 event 就是事件对象，我们还喜欢的写成 e 或者 evt 
} 
eventTarget.addEventListen\er('click', function(event) {
})
```

事件对象也有兼容性问题：ie678 通过 window.event 

兼容性的写法  e = e || window.event;



**事件对象的常见属性和方法**

```javascript
e.target	    返回触发事件的对象 标准
e.srcElement	返回触发事件的对象 非标准 ie6-8使用
e.type	        返回事件的类型 比如click mouseover 不带on
e.cancelBubble	该属性阻止冒泡，非标准，ie6-8使用
e.returnValue	该属性阻止默认行为 非标准，ie6-8使用
e.preventDefault()	该方法阻止默认行为 标准 比如不让链接跳转
e.stopPropagation()	阻止冒泡 标准
```



**e.target 和 this 的区别**

e.target 返回的是触发事件的对象（元素），this 返回的是绑定事件的对象（元素）

```html
<ul>
    <li>123</li>
    <li>123</li>
    <li>123</li>
</ul>
<script>
    var ul = document.querySelector('ul');
    ul.addEventListener('click', function(e) {
        console.log(this);        //<ul>.....</ul>
        console.log(e.target);    //<li>123</li>
    })
</script>
```



### 5. 事件对象阻止默认行为

链接不跳转，或者让提交按钮不提交

```html
<a href="http://www.baidu.com">百度</a>
<script>
    var a = document.querySelector('a');
    a.addEventListener('click', function(e) {
        e.preventDefault();
    })
    
    // 传统的注册方式
    a.onclick = function(e) {
        // 普通浏览器
        e.preventDefault();
        // 低版本浏览器 ie678
        e.returnValue;
        // return false,没有兼容性问题,只限于传统的注册方式
        return false;
    }
</script>
```



### 6. 阻止事件冒泡

:star:面试中经常问到的问题

事件冒泡：开始时由最具体的元素接收，然后逐级向上传播到到 DOM 最顶层节点

```javascript
e.stopPropagation();    //标准写法
e.cancelBubble = true;  //非标准写法
```

```javascript
var son = document.querySelector('.son');
son.addEventListener('click', function(e) {
    alert('son');
    e.stopPropagation();
    e.cancelBubble = true;
}, false);
```



### 7. 事件委托

:star:事件委托的原理：不是每个子节点单独设置事件监听器，而是事件监听器设置在其父节点上，然后利用冒泡原理影响设置每个子节点

作用：只操作了一次DOM，提高了程序性能

以下案例：给 ul 注册点击事件，然后利用事件对象的 target 来找到当前点击的 li，因为点击 li，事件会冒泡到 ul 上， ul 有注册事件，就会触发事件监听器。

```html
<ul>
    <li>知否知否，点我应有弹框在手！</li>
    <li>知否知否，点我应有弹框在手！</li>
    <li>知否知否，点我应有弹框在手！</li>
    <li>知否知否，点我应有弹框在手！</li>
    <li>知否知否，点我应有弹框在手！</li>
</ul>
<script>
    var ul = document.querySelector('ul');
    ul.addEventListener('click', function(e) {
        alert('知否知否');
        
        // e.target 这个可以得到我们点击的对象
        // 点了谁，就让谁的style里面的backgroundColor颜色变为pink
        e.target.style.backgroundColor = 'pink';
    })
</script>
```



### 8. 常用的鼠标事件

| 鼠标事件    | 触发条件                     |
| ----------- | ---------------------------- |
| onclick     | 鼠标点击左键触发             |
| onmouseover | 鼠标经过触发                 |
| onmouseout  | 鼠标离开触发                 |
| onfocus     | 获得鼠标焦点触发             |
| onblur      | 失去鼠标焦点触发             |
| onmousemove | 鼠标移动触发                 |
| onmouseup   | 鼠标弹起触发                 |
| onmousedown | 鼠标按下触发                 |
| contextmenu | 主要用于取消默认的上下文菜单 |
| selectstart | 用于禁止鼠标选中             |

禁止鼠标右键与鼠标选中

```html
<h1>我是一段不愿意分享的文字</h1>
<script>
    // 1. contextmenu
    document.addEventListener('contextmenu', function(e) {
        e.preventDefault(); // 阻止默认行为
    })
    // 2. selectstart
    document.addEventListener('selectstart', function(e) {
        e.preventDefault();
    })
</script>
```



**鼠标事件对象**：

| 鼠标事件对象    | 说明                                       |
| --------------- | ------------------------------------------ |
| e.clientX       | 鼠标相对于<u>浏览器窗口可视区</u>的X坐标   |
| e.clientY       | 鼠标相对于<u>浏览器窗口可视区</u>的Y坐标   |
| e.pageX（重点） | 鼠标相对于<u>文档页面</u>的X坐标 IE9+ 支持 |
| e.pageY（重点） | 鼠标相对于<u>文档页面</u>的Y坐标 IE9+ 支持 |
| e.screenX       | 鼠标相对于<u>电脑屏幕</u>的X坐标           |
| e.screenY       | 鼠标相对于<u>电脑屏幕</u>的Y坐标           |

```javascript
document.addEventListener('click', function(e) {
    console.log(e.clientX);
    console.log(e.clientY);

    console.log(e.pageX);
    console.log(e.pageY);

    console.log(e.screenX);
    console.log(e.screenY);
})
```

案例：跟随鼠标移动的图片

```html
<head>  
    <style>
        img {
            height: 140px;
            width: 120px;
            position: absolute;
        }
    </style>
</head>
<body>
    <img src="C:\Users\lenovo\Pictures\IMG_3554.PNG" />
    <script>
        var pic = document.querySelector('img')
        document.addEventListener('mousemove', function (e) {
            var x = e.pageX
            var y = e.pageY
            pic.style.left = x - 70 + 'px'
            pic.style.top = y - 60 + 'px'
        })
    </script>
</body>
```



### 9. 常用的键盘事件

| 键盘事件   | 触发条件                                                     |
| ---------- | ------------------------------------------------------------ |
| onkeyup    | 某个键盘按键被松开时触发                                     |
| onkeydown  | 某个键盘按键被按下时触发                                     |
| onkeypress | 某个键盘按键被按下时触发，但是它不识别功能键，比如 ctrl shift 左右箭头 |

```javascript
document.addEventListener('keyup', function() {
    console.log('我弹起了');
})

document.addEventListener('keypress', function() {
    console.log('我按下了press');
})

document.addEventListener('keydown', function() {
    console.log('我按下了down');
})
```

三个事件的执行顺序  keydown ---> keypress ---> keyup



**键盘事件对象：**

| 键盘事件对象 | 说明                |
| ------------ | ------------------- |
| keyCode      | 返回该键值的ASCII值 |

keyup 和 keydown 事件不区分字母大小写，a 和 A 得到的都是65

keypress 事件区分字母大小写，a 97，A 65

```javascript
document.addEventListener('keyup', function(e) {
    console.log('up:' + e.keyCode);
})
document.addEventListener('keypress', function(e) {
    console.log('press:' + e.keyCode);
})
```

案例1：按键focus输入框 

search.focus()

案例2：输入数字显示大字

con.style.display = 'none';

con.style.display = 'block';

