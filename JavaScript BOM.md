# JavaScript进阶 | BOM

caiyi 2021/8/10

## 一、概述

BOM = Browser Object Model 

它提供了独立于内容而与浏览器窗口进行交互的对象，其核心对象是 window

![image-20210811101919656](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210811102050.png)

我想开个热点

BOM的构成：

![image-20210811102128830](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210811102130.png)

window 对象是浏览器的顶级对象，它具有双重角色：

1. 它是 JS 访问浏览器窗口的一个接口
2. 它是一个全局对象。定义在全局作用域中的变量、函数都会变成 window 对象的属性和方法
3. 在调用的时候可以省略 window，如 *window.alert()  window.prompt()*
4. 注意：window 的一个特殊属性 *window.name*

```javascript
// 定义在全局作用域中的变量会变成window对象的属性
var num = 10;
console.log(window.num);

// 定义在全局作用域中的函数会变成window对象的方法
function fn() {
    console.log(11);
}
window.fn();

//不要用这个name变量,window下有一个特殊属性window.name
console.log(window.name); //空的字符串，不会报错
```



## 二、window 对象的常见事件

### 1. 窗口加载事件

```javascript
window.onload = function(){}
window.addEventListener('load',function(){})
document.addEventListener('DOMContentLoaded',function(){})
```



- ==*window.onload*== 是窗口加载事件，当文档内容完全加载完成会触发该事件（包括图像，脚本文件，CSS文件等），就调用的处理函数

  - 有了 *window.onload* 就<u>可以把JS代码写到页面元素的上方</u>

  - *window.onload* 是传统注册事件方式，只能写一次
  - 如果有多个，会以最后一个 *window.onload* 为准

- ==*window.addEventListener*== 与 *window.onload* 不同的是，可以注册多次事件不会冲突和覆盖

- ==*DOMCountentLoaded*== 事件触发时，仅当DOM加载完成，不包括样式表，图片，flash等等

  - 如果页面的图片很多的话, 从用户访问到 onload 触发可能需要较长的时间

  - *DOMContentLoaded* 是DOM加载完毕，不包含图片 flash css 等就可以执行，加载速度比load更快一些

    

```javascript
window.onload = function() {
    var btn = document.querySelector('button');
    btn.addEventListener('click', function() {
        alert('点击我');
    })
}
window.onload = function() {
    alert(22); //只弹出22
}

window.addEventListener('load', function() {
    var btn = document.querySelector('button');
    btn.addEventListener('click', function() {
        alert('点击我');
    })
})
window.addEventListener('load', function() {
    alert(22); //同时弹出 22 和 点击我
})

document.addEventListener('DOMContentLoaded', function() {
    alert(33); // 33 最先弹出
})
```



### 2. 调整窗口大小事件

调整窗口大小加载事件，当触发时就调用的处理函数

我们经常利用这个事件完成响应式布局

```javascript
window.onresize = function() {}
window.addEventListener('resize',function(){});
```

==*window.innerWidth*==：当前屏幕的宽度



```html
<script>
    window.addEventListener('load', function() {
        var div = document.querySelector('div');
        window.addEventListener('resize', function() {
            if (window.innerWidth <= 800) {
                div.style.display = 'none';
            } else {
                div.style.display = 'block';
            }
        })
    })
</script>
<div></div>
```



## 三、定时器



### 1. setTimeout()定时器

用于设置一个定时器，该定时器在定时器到期后执行调用函数

```javascript
window.setTimeout(调用函数,毫秒数);
```

1. *window* 在调用的时候可以省略

2. 延时时间单位是毫秒 但是可以省略，如果省略默认的是0

3. 页面中可能有很多的定时器，我们经常给定时器加标识符

4. *setTimeout()* 这个调用函数我们也称为**回调函数** callback：普通函数是按照代码顺序直接调用，而这个函数，需要等待事件，事件到了才会去调用这个函数，因此称为回调函数

   

```javascript
function callback() {
    console.log('爆炸了');
}
var timer1 = setTimeout(callback, 3000);
var timer2 = setTimeout(callback, 5000);
```



### 2. clearTimeout()停止定时器

*clearTimeout()* 方法取消了先前通过调用  *setTimeout()* 建立的定时器

```javascript
window.clearTimeout(timeoutID) //里面的参数就是定时器的标识符
```

```javascript
var btn = document.querySelector('button');
var timer = setTimeout(function() {
    console.log('boom');
}, 5000);
btn.addEventListener('click', function() {
    clearTimeout(timer);
})
```



### 3. setInterval() 定时器

重复调用一个函数，每隔这个时间，就去调用一次回调函数

```javascript
window.setInterval(回调函数,间隔毫秒数);

setInterval(function() {
    console.log('继续输出');
}, 1000);
```

区别：

*setTimeout*  延时时间到了就去调用这个回调函数，只调用一次就结束了这个定时器

*setInterval*  每隔这个延时时间就去调用这个回调函数，会调用很多次，重复调用这个函数



### 4. clearInterval()停止定时器

取消了先前通过调用  *setInterval()*  建立的定时器

里面的参数就是定时器的标识符

```
clearInterval(timerID);
```



```html
<button class="begin">开启定时器</button>
<button class="stop">停止定时器</button>
<script>
    var begin = document.querySelector('.begin');
    var stop = document.querySelector('.stop');
    var timer = null; // 全局变量  null是一个空对象
    begin.addEventListener('click', function() {
        timer = setInterval(function() {
            console.log('ni hao ma');
        }, 1000);
    })
    stop.addEventListener('click', function() {
        clearInterval(timer);
    })
</script>
```



### 5. this 指向

- 全局作用域或者普通函数中 this 指向全局对象 window (注意定时器里面的this指向window)
- 方法调用中谁调用 this 指向谁
- 构造函数中 this 指向构造函数实例

```javascript
//1. 全局作用域或者普通函数中 this 指向 window
console.log(this); //window

function fn() {
    console.log(this);
}
window.fn(); //window

window.setTimeout(function() {
    console.log(this);
}, 1000);  //window

// 2. 方法调用中谁调用this指向谁
var o = {
    sayHi: function() {
        console.log(this); // this指向的是 o 这个对象
    }
}
o.sayHi();
var btn = document.querySelector('button');
btn.addEventListener('click', function() {
    console.log(this); // this指向的是btn这个按钮对象
})

// 3. 构造函数中this指向构造函数的实例
function Fun() {
    console.log(this); // this 指向的是fun实例对象
}
var fun = new Fun();
```



### 6. 案例

- 倒计时效果 P84

- 发送短信案例 P86

  ```html
  <button>send</button>
  <script>
      var btn = document.querySelector('button')
      var time = 5
      btn.addEventListener('click', function () {
          btn.disabled = true
          var timer = setInterval(() => {
              if (time == 0) {
                  clearInterval(timer)
                  btn.disabled = false
                  btn.innerHTML = 'send'
                  time = 5
              } else {
                  btn.innerHTML = '还剩' + time + 's'
                  time--
              }
          }, 1000)
          })
  </script>
  ```





## 四、JS执行队列



### 1. JS是单线程

JavaScript 语言的一大特点就是单线程，同一个时间只能做一件事

这是因为 Javascript 这门脚本语言诞生的使命所致——JavaScript 是为处理页面中用户的交互，以及操作 DOM 而诞生的。比如我们对某个 DOM 元素进行添加和删除操作，不能同时进行。 应该先进行添加，之后再删除

单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务



### 2. 同步和异步

问题引入：

```javascript
console.log(1);
setTimeout(function() {
    console.log(3);
},1000);
console.log(2);
// 结果是 1 2 3

console.log(1);
setTimeout(function() {
    console.log(3);
},0);
console.log(2);
//结果是 1 2 3 
```

利用多核 CPU 的计算能力，HTML5 提出 Web Worker 标准，允许 JavaScript 脚本创建多个线程，于是，JS 中出现了同步和异步：

- 同步：前一个任务结束后再执行后一个任务
- 异步：在做这件事的同时，你还可以去处理其他事情



### 3. 执行队列

**同步任务**：同步任务都在主线程上执行，形成一个 <u>执行栈</u>

**异步任务**：JS中的异步是通过 <u>回调函数</u> 实现的，异步任务相关回调函数添加到 <u>任务队列</u> 中

异步任务有以下三种类型：

- 普通事件，如 *click, resize* 等
- 资源加载，如 *load, error* 等
- 定时器，包括 *setInterval, setTimeout* 等



**执行过程详解**：

1. 先执行 <u>执行栈</u> 中的同步任务
2. 异步任务(回调函数)放入 <u>任务队列</u> 中
3. 一旦执行栈中的所有同步任务执行完毕，系统就会按次序读取任务队列中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈，开始执行

![image-20210811145636497](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812135039.png)

4. 同步任务放在执行栈中执行，异步任务由异步进程处理放到任务队列中，执行栈中的任务执行完毕会去任务队列中查看是否有异步任务执行，由于主线程不断的重复获得任务、执行任务、再获取任务、再执行，所以这种机制被称为 **<u>事件循环</u>**

![image-20210811145801197](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812135057.png)



![image-20210811150015836](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812135048.png)





## 五、location对象

*location* 属性用于获取或者设置窗体的url，并且可以解析url

因为这个属性返回的是一个对象，所以我们将这个属性也称为 location 对象。

### 1. URL

==统一资源定位符==（uniform resouce locator）：是互联网上标准资源的地址，互联网上的每个文件都有一个唯一的 URL，它包含的信息指出 <u>文件的位置</u> 以及 <u>浏览器应该怎么处理它</u>。

**url的一般格式**：

```
protocol://host[:port]/path/[?query]#fragment

http://www.itcast.cn/index.html?name=andy&age=18#link
```

| url组成  | 说明                                    |
| -------- | --------------------------------------- |
| protocol | 通信协议 常用的http,ftp,maito等         |
| host     | 主机(域名) www.itheima.com              |
| port     | 端口号，省略时为默认端口号80            |
| path     | 路径，由'/'符号隔开，目录或文件地址     |
| query    | 参数，以键值对的形式，通过&符号分隔开来 |
| fragment | 片段，#后面内容，常见于链接、锚点       |



### 2. location对象属性

```
对象属性	        返回值
location.href	   获取或者设置整个URL
location.host	   返回主机（域名）www.baidu.com
location.port	   返回端口号，如果未写返回空字符串
location.pathname  返回路径
location.search	   返回参数
location.hash	   返回片段 #后面内容常见于链接 锚点
```

重点记住： *href，search*



小案例：5s之后跳转页面

```html
<div></div>
<script>
    var div = document.querySelector('div');
    var timer = 5;
    setInterval(function() {
        if (timer == 0) {
            location.href = 'http://www.itcast.cn';
        } else {
            div.innerHTML = '您将在' + timer + '秒钟之后跳转到首页';
            timer--;
        }

    }, 1000);
</script>
```



### 3. 获取URL参数

主要练习数据在不同页面中的传递

我们简单写一个登录框，点击登录跳转到 index.html

```html
<body>
    <form action="index.html">  <!--action表示提交后跳转到哪里-->
        用户名： <input type="text" name="uname">
        <input type="submit" value="登录">
    </form>
</body>
```

接下来我们写 index.html

```html
<body>
    <div></div>
    <script>
        console.log(location.search); // ?uname=andy
        // substr(起始的位置，截取几个字符);
        var params = location.search.substr(1); // uname=andy
        console.log(params);
        
        // 2.把字符串分割为数组 split('=');
        var arr = params.split('=');
        console.log(arr); // ["uname", "ANDY"]
        var div = document.querySelector('div');
        
        // 3.把数据写入div中
        div.innerHTML = arr[1] + '欢迎您';
    </script>
</body>
```

这样我们就能获取到路径上的URL参数



### 4. location对象方法

```
对象方法	         返回值
location.assign()	跟href一样，可以跳转页面（也称为重定向页面）,可以记录历史，有后退功能
location.replace()	替换当前页面，因为不记录历史，所以不能后退页面
location.reload()	重新加载页面，相当于刷新按钮或者 f5 ，如果参数为true 强制刷新 ctrl+f5
```

```html
<button>点击</button>
<script>
    var btn = document.querySelector('button');
    btn.addEventListener('click', function() {
        // 记录浏览历史，所以可以实现后退功能
        location.assign('http://www.itcast.cn');
        // 不记录浏览历史，所以不可以实现后退功能
        location.replace('http://www.itcast.cn');
        location.reload(true);
    })
</script>
```





## 六、navigator对象

avigator 对象包含有关浏览器的信息，它有很多属性

我们常用的是 *==userAgent==*, 该属性可以返回由客户机发送服务器的 ==*user-agent*== 头部的值

下面 JavaScript 代码可以判断用户是用哪个终端打开页面的，如果是用 PC 打开的，就跳转到 PC 端的页面，如果是用手机打开的，就跳转到手机端页面

```javascript
if((navigator.userAgent.match(/(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i))) {
    window.location.href = "";     //手机
 } else {
    window.location.href = "";     //电脑
 }
```



## 七、history对象

window 给我们提供了一个 history 对象，与浏览器历史记录进行交互

该对象包含用户（在浏览器窗口中）访问过的 URL

| history对象方法 | 作用                                                         |
| --------------- | ------------------------------------------------------------ |
| back()          | 可以后退功能                                                 |
| forward()       | 前进功能                                                     |
| go(参数)        | 前进后退功能，参数如果是 1 前进1个页面 如果是 -1 后退1个页面 |

```html
<a href="list.html">点击我去往列表页</a>
<button>前进</button>
<script>
    var btn = document.querySelector('button');
    btn.addEventListener('click', function() {
        // history.forward();
        history.go(1);
    })
</script>
```

