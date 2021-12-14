# Android studio

zcy 2021/8/14



## 一、开始启程

### 1. 认识Android

Android 大致可以分为4层架构：Linux内核层、系统运行库层、应用框架层和应用层

Android系统四大组件分别是Activity、Service、BroadcastReceiver和 ContentProvider

Android系统还自带了这种轻量级、运算速度极快的嵌入式关系型数据库， SQLite数据库，它不仅支持标准 的SQL语法，还可以通过Android封装好的API进行操作



### 2. 创建项目

![image-20210814140036526](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210814140038.png)

**Package name**：表示项目的包名，Android系统就是通过包名来区分不同应用程序的，因此包名一定要具有唯一性

**Language**：这里默认选择了Kotlin。在过去，Android应用程序只能使用 Java来进行开发，本书的前两个版本也都是用Java语言讲解的。然而在2017年，Google引入 了一款新的开发语言——Kotlin，并在2019年正式向广大开发者公布了Kotlin First的消息

**Minimum API level**：设置项目的最低兼容版本，Android 5.0以 上的系统已经占据了超过85%的Android市场份额，因此这里我们将Minimum SDK指定成API 21就可以了



### 3. 分析第一个Android程序结构

#### 3.1  Project模式的项目结构

![image-20210814115507396](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210814115516.png)

**.gradle和.idea**：放置的都是Android Studio自动生成的一些文件

**app**：项目中的代码、资源等内容都是放置在这个目录下的，我们后面的开发工作也基本是在这 个目录下进行的

**gradle**：这个目录下包含了gradle wrapper的配置文件，使用gradle wrapper的方式不需要提前将gradle下载好，而是会自动根据本地的缓存情况决定是否需要联网下载gradle。Android Studio默认就是启用gradle wrapper方式的，如果需要更改成离线模式，可以点击Android Studio导航栏→ File → Settings → Build, Execution, Deployment → Gradle，进行配置更改

**gitignore**：用来将指定的目录或文件排除在版本控制之外的

 **build.gradle**：项目全局的gradle构建脚本

**gradle.properties**：全局的gradle配置文件

**gradlew和gradlew.bat**：用来在命令行界面中执行gradle命令的，其中gradlew是在Linux或Mac系统，gradlew.bat是在Windows系统

 **local.properties**：指定本机中的Android SDK路径

 **settings.gradle**：指定项目中所有引入的模块



#### 3.2 app目录下的结构

![image-20210814135809352](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210814135811.png)

**build**：包含了一些在编译时自动生成的文件

**libs**：放置第三方jar包

**androidTest**：编写测试用例

**java**：放置我们所有Java代码的地方（Kotlin代码也放在这里）

**res**：项目中使用到的所有图片、布局、字符串等资源

**AndroidManifest.xml**：是整个Android项目的配置文件，你在程序中定义的所有四大组件都需要在这个文件里注册

**test**：编写Unit Test测试用例



接下来分析一下HelloWorld项目究竟是**如何运行起来**的：

首先打开 ==AndroidManifest.xml==，这段代码表示对MainActivity进行注册，intent-filter里的两行代码表示MainActivity是这个项目的主Activity

```xml
<activity android:name=".MainActivity">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
```

打开 ==MainActivity==, 首先MainActivity是继承自AppCompatActivity (AndroidX中提供的一种向下兼容的Activity)，MainActivity中有一个onCreate()方法，里面调用了setContentView()方法，给当前的Activity引入了一个activity_main布局

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```

打开 ==activity_main.xml==，在 TextView中看到了“Hello World”的字样，因为Android程序的设计讲究逻辑和视图分离，不推荐在Activity中直接编写界面，而是在布局文件中编写界面

```xml
<androidx.constraintlayout.widget.ConstraintLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!" />

</androidx.constraintlayout.widget.ConstraintLayout>
```



#### 3.3 res目录下的结构

![image-20210814141631508](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210814141633.png)

以“drawable”开头的目录：用来放图片的

以“mipmap”开头的目录：用来放应用图标的

以“values”开头的目录：放字符串、样式、颜色等配置的

以“layout”开头的目录：放布局文件

我们应该如何使用这些资源呢，以字符串为例，这里定义了一个应用程序名的字符串，我们有以下两种方式来引用它

![image-20210814142241326](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210814142244.png)

1. 在代码中通过R.string.app_name可以获得该字符串的引用。
2. 在XML中通过@string/app_name可以获得该字符串的引用



### 4. 一些error解决方法

[ERROR: SSL peer shut down incorrectly错误解决(Android Studio)](https://www.cnblogs.com/rainbow70626/p/14337649.html)

错误信息：ERROR: SSL peer shut down incorrectly

错误原因：是studio工具不支持https请求

方法一：右上角 SDK Manager 进入到窗口里面 → 选择 SDK Update Sites 这个选项 → 勾选下方的 Force https// sources to be fetched using http// 选项 → 重启Android Studio → 点击右上大象图标重新下载

![image-20210814140531446](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210814140533.png)

方法二：

将 gradle-wrapper.properties 文件里面的 distributionUrl=https 中的 https 改成 http，然后重新点击上方的按钮大象重新下载gradle文件

![image-20210814140708805](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210814140710.png)



## 二、探究Activity

Activity是一种可以包含用户界面的组件，主要用于和用户进行交互

### 1. 活动的基本用法

#### 1.1 创建活动

![image-20210814162357857](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210814162359.png)

Generate Layout File：会自动创建一个对应的布局文件

Launcher Activity：会自动将这个Activity设置为当前项目的主Activity

项目中的任何Activity都应该重写onCreate()方法，调用setContentView()方法来给当前的Activity加载一个布局，我们一般会传入一个布局文件的id

```java
public class SecondActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
    }
}
```

#### 1.2 Toast

在程序中可以使用它将一些短小的信息通知给用户，一段时间后自动消失

在activity_main中添加一个button，并赋予id button_1

```XML
<Button
    android:id="@+id/button_1"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:text="click"/>
```

在 onCreate() 方法中添加如下代码：

通过 ==findViewById()== 获取在布局文件中定义的button_1，该方法返回的是一个继承自View的泛型对象，因此需要向下转型成Button对象

通过调用 ==setOnClickListener()== 方法为按钮注册一个监听器，点击按钮时就会执行监听器中的 ==onClick()== 方法，Toast的功能在  onClick() 方法中编写了

```JAVA
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    Button btn = (Button) findViewById(R.id.button_1);
    btn.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            Toast.makeText(MainActivity.this,"you clicked btn1",
                           Toast.LENGTH_SHORT).show();
        }
    });
}
```

Toast的用法：

通过静态方法 ==makeText()== 创建出一个Toast对象，然后调用 ==show()== 将Toast显示出来

第一个参数是Context，就是Toast要求的上下文，Activity本身就是一个Context对象，因此这里直接传入this。第二个参数是Toast显示的文本内容。第三个参数是Toast显示的时长，有两个内置常量可以选择：Toast.LENGTH_SHORT 和 Toast.LENGTH_LONG



#### 1.3 Menu

 在res目录下新建一个menu文件夹，在menu文件夹下新建一个菜单文件 main.xml，代码如下，我们用 <item> 创建了两个菜单项

```xml
<menu xmlns:android="http://schemas.android.com/apk/res/android">

    <item
        android:id="@+id/add_item"
        android:title="add"></item>
    <item
        android:id="@+id/remove_item"
        android:title="remove"></item>
</menu>
```

接着回到 MainActivity 来重写 ==onCreateOptionsMenu()== 方法，==getMenuInflater()== 方法能够得到一 个MenuInflater 对象，再调用它的 ==inflate()== 方法，就可以给当前Activity创建菜单了

inflate() 两个参数：第一个参数指定我们通过哪一个资源文件来创建菜单，第二个参数指定菜单项将添加到哪一个Menu对象当中，这里直接使用 onCreateOptionsMenu() 方法中传入的menu参数

返回 true，表示允许创建的菜单显示出来

```java
@Override
public boolean onCreateOptionsMenu(Menu menu){
    getMenuInflater().inflate(R.menu.main,menu);
    return true;
}
```

我们继续给菜单定义响应事件

在 MainActivity中重写 ==onOptionsItemSelected()== 方法，调用item.itemId来判断点击的是哪一个菜单项

```java
@Override
public boolean onOptionsItemSelected(MenuItem item){
    switch (item.getItemId()) {
        case R.id.add_item:
            Toast.makeText(this, "You clicked Add",
                           Toast.LENGTH_SHORT).show();
            break;
        case R.id.remove_item:
            Toast.makeText(this, "You clicked Remove",
                           Toast.LENGTH_SHORT).show();
            break;
        default:
    }
    return true;
}
```

效果图如下

![image-20210814172207794](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210814172231.png)



#### 1.4 销毁一个活动

按一下Back键，或者z在代码里使用 finish() 方法

```java
btn.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        finishi();
    }
});
```



### 2. Intent 在活动之间穿梭

由一个Activity跳转到另一个Activity

#### 2.1 Intent简介

Intent是Android程序中各组件之间进行交互的一种方式，不仅可以指明当前组件想要执行的动作，还可以在不同组件之间传递数据，一般可用于启动Activity、启动Service以及发送广播等场景

#### 2.2  显式Intent

新建 SecondActivity.java 和 acitvity_second.xml，在布局文件里加上按钮id button_2

通过 ==Intent()== 构造函数就可以构建出 Intent 对象的“意图”，第一个参数传入 MainActivity.this 作为上下文，第二个参数传入 SecondActivity.class 作为目标 Activity

Activity类中提供了一个 ==startActivity()== 方法，接收一个Intent参数，专门用于启动Activity

```java
Button btn = (Button) findViewById(R.id.button_1);
btn.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        Intent intent = new Intent(MainActivity.this,SecondActivity.class);
        startActivity(intent);
    }
});
```

#### 2.3 隐式Intent

指定了一系列的action和category等信息，交由系统去分析这个Intent，找出合适的Activity去启动

打开 ==AndroidManifest.xml==，通过在标签 <activity> 下配置 <intent-filter> 的内容，可以指定 SecondActivity 能够响应的 action 和 category

```xml
<activity android:name=".SecondActivity">
    <intent-filter>
        <action android:name="com.example.chapter2.ACTION_START" />
        <category android:name="android.intent.category.DEFAULT" />
    </intent-filter>
</activity>
```

修改MainActivity中按钮的点击事件，只有 <action> 和 <category> 中的内容同时匹配Intent构造函数中指定的action和category时，这个Activity才能响应该Intent

```java
btn.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        Intent intent = new Intent("com.example.chapter2.ACTION_START");
        startActivity(intent);
    }
});
```

这里没有指定 category 是因为 DEFAULT 是一种默认的 category，调用函数时会自动添加进去

每个Intent中只能指定一个action，但能指定多个 category，在 MainActivity.java 里面调用 ==intent.addCategory()==，再在SecondActivity的 <intent-filter>加上一个新的 <category>，否则会报错

```java
Intent intent = new Intent(MainActivity.this,SecondActivity.class);
intent.addCategory("com.example.chapter2.MY_CATEGORY");
startActivity(intent);
```

```XML
<action android:name="com.example.chapter2.ACTION_START" />
<category android:name="com.example.chapter2.MY_CATEGORY"/>
<category android:name="android.intent.category.DEFAULT" />
```



#### 2.4 更多隐式Intent的用法

不仅可以启动自己程序内的Activity，还可以启动其他程序的Activity

- **Intent.ACTION_VIEW**

  首先指定了Intent的action是Intent.ACTION_VIEW，然后通过==Uri.parse()==方法将一个网址字符串解析成一个Uri对象，再调用Intent的 ==setData()== 方法将这个Uri对象传递进去

  ```java
  btn.setOnClickListener(new View.OnClickListener() {
      @Override
      public void onClick(View view) {
          Intent intent = new Intent(Intent.ACTION_VIEW);
          intent.setData(Uri.parse("https://www.baidu.com"));
          startActivity(intent);
      }
  });
  ```

  

- **Intent.ACTION_DIAL**

  ```java
  btn.setOnClickListener(new View.OnClickListener() {
      @Override
      public void onClick(View view) {
          Intent intent = new Intent(Intent.ACTION_DIAL);
          intent.setData(Uri.parse("tel:10086"));
          startActivity(intent);
      }
  });
  ```

  点击按钮效果如图

  ![image-20210815104512937](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210815104512937.png)



#### 2.5 向下一个activity传递数据

Intent中提供了一系列 ==putExtra()== 方法的重载，可以把我们想要传递的数据暂存在Intent中，在启动另一个Activity后，只需要把这些数据从Intent中取出就可以了



例如要把MainActivity中的字符串传递到SecondActivity中：

使用显式Intent的方式来启动SecondActivity，并通过 ==putExtra()== 方法传递了一个字符串，第一个参数是键，用于之后从 Intent 中取值，第二个参数才是真正要传递的数据

```java
btn1.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        String data = "this is from MainActivity";
        Intent intent = new Intent(MainActivity.this,SecondActivity.class);
        intent.putExtra("extra_data",data);
        startActivity(intent);
    }
});
```

在 SecondActivity中，调用父类的 ==getIntent()== 方法，获取用于启动 SecondActivity的Intent，然后调用 ==getStringExtra()== 方法传入相应的键值

传递字符串：getStringExtra()

传递整型数据：getIntExtra()

传递布尔值：getBooleanExtra()

```java
public class SecondActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
        
        Intent intent = getIntent();
        String data = intent.getStringExtra("extra_data");
        Log.d("SecondActivity",data);
    }
}
```



#### 2.6 返回数据给上一个活动

 Activity有一个用于启动Activity的 startActivityForResult() 方法，它期望在Activity销毁的时候能够返回一个结果给上一个Activity



**① 修改MainActivity代码**

用 ==startActivityForResult()== 来启动活动，第一个参数还是Intent，第二个参数是请求码，用于在之后的回调中判断数据的来源

```java
btn1.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        Intent intent = new Intent(MainActivity.this,SecondActivity.class);
        startActivityForResult(intent,1);
    }
});
```

在 SecondActivity被销毁之后会回调上一个Activity的 ==onActivityResult()== 方法，第一个参数是在启动 Activity 时传入的请求码，第二个参数是在返回数据时传入的处理结果；第三个参数即携带着返回数据的Intent

```java
@Override
protected void onActivityResult(int rqCode, int resCode, Intent data) {
    switch (rqCode) {
        case 1:
            if(resCode == RESULT_OK) {
                String returnData = data.getStringExtra("data_return");
                Log.d("MainActivity",returnData);
            }
    }
}
```



**② 修改SecondActivity代码：**

构建一个Intent对象，仅用来传递数据，不指定任何意图

后调用了==setResult()==方法，专门用于向上一个Activity返回数据。第一个参数用于向上一个Activity返回处理结果（RESULT_OK 或 RESULT_CANCELED），第二个参数把带有数据的Intent传递回去

```java
Button btn2 = (Button) findViewById(R.id.button_2);
btn2.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        Intent intent = new Intent();
        intent.putExtra("data_return","this is from SecondActivity");
        setResult(RESULT_OK,intent);
        finish();
    }
});
```

如果用户在SecondActivity中并不是通过点击按钮，而是通过按下Back键回到 FirstActivity，通过在SecondActivity中重写 ==onBackPressed()== 方法来解决

```java
@Override
public void onBackPressed(){
    Intent intent = new Intent();
    intent.putExtra("data_return","this is from SecondActivity");
    setResult(RESULT_OK,intent);
    finish();
}
```



### 3. 活动的生命周期

#### 3.1 返回栈

Android中的Activity是可以层叠的，新活动覆盖在旧活动上

Android是使用任务（task）来管理Activity的，一个任务就是一组存放在栈里的Activity 的集合，这个栈称作返回栈（back stack）

![image-20210815114237461](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210815114237461.png)



#### 3.2 Activity状态

- 运行：位于返回栈的顶部，系统最不愿意回收
- 暂停：不在栈顶，但仍可见(例如对话框的背后)，暂停状态仍是完全存活的，系统不愿意回收
- 停止：不在栈顶，完全不可见，系统仍保为这个活动保存状态和成员变量，但在内存紧张会被回收
- 销毁：从返回栈移除，系统倾向回收，节约内存



#### 3.3 Activity生存期

完整生存期 ，onCreate —— onDestroy，初始化 —— 释放内存

可见生存期，onStart —— onStop，不可见 —— 可见时调用

前台展示生存期，onResume —— onPause



- onCreate，初始化，比如加载布局、绑定事件

- onStart，不可见到可见时调用

- onResume，和用户交互前进行调用，此时一定位于栈顶，处于运行状态

- onPause，在系统切换到另一个ACT时调用

- onStop，完全不可见时调用

- onDestroy，在销毁前被调用

- onRestart，从停止变为运行时调用，也就是Activity 被重新启动了

  

![image-20210815115026563](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210815115026563.png)



#### 3.4 活动被回收了怎么办

Activity被回收前，系统会调用一个方法==onSaveInstanceState()==来保存用户的数据，在 onPause 和onStop 之间，解决活动被回收临时数据得不到保留的问题

在 MainActivity 中写入函数

```java
@Override
protected void onSaveInstanceState(Bundle outState){
    super.onSaveInstanceState(outState);
    String temp = "something you just typed";
    outState.putString("data_kay",temp);
}
```

我们一直使用的onCreate()方法也有一个Bundle参数，如果在Activity被系统回收之前，通过onSaveInstanceState()方法保存数据，这个参数就会带有之前保存的全部数据，只需要将数据取出即可

```java
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    if(savedInstanceState != null){
        String temp = savedInstanceState.getString("data_key");
        log.d(TAG,temp);
    }
}
```



### 4.  活动的启动模式

在实际项目中我们应该根据特定的需求为每个Activity指定恰当的启动模式，可以在AndroidManifest.xml中通过给标签指定 android:launchMode 属性来选择启动模式

- standard，默认的启动模式，每次创建都会产生一个新的，放在栈顶，不在乎以前是否创建过(单体可循环，默认情况)

- singleTop，每次创建时，如果发现栈顶是本身，就不再创建，否则就创建（交替可循环）

  ```xml
  android:launchMode="singleTop"
  ```

- singleTask，每次启动，系统首先会在返回栈中检查是否存在该Activity，如果已经存在则直接使用该实例， 并把在这个Activity之上的所有其他Activity统统出栈

- singleInstance，真正单态模式，自身拥有一个返回栈





## 三、UI开发的点滴

### 1. 常用控件的使用方法

#### 1.1 TextView

```xml
<TextView
          android:id="@+id/textView"
          android:layout_width="match_parent"
          android:layout_height="wrap_content"
          android:gravity="center"
          android:text="This is TextView"/>
```

android:id  定义唯一标识符

android:text  文本内容

android:textColor  文字的颜色

android:textSize  文字的大小，文字大小使用sp作为单位

android:layout_width  控件的宽度

android:layout_height  控件的高度（match_parent、wrap_content、固定值，单位一般用dp）

android:gravity  文字的对齐方式（top、bottom、start、 end、center、center_vertical、center_horizontal）

#### 1.2 Button

```xml
<Button
        android:id="@+id/button"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Button" />
```

android:textAllCaps="false"  系统就会保留你指定的原始文字内容

在MainActivity中为Button的点击事件注册一个监听器

```java
Button btn1 = (Button) findViewById(R.id.button_1);
btn1.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        //在此处添加逻辑
    }
});
```

如果不喜欢匿名注册，也可以使用实现接口的方式来进行注册

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    Button btn1 = (Button) findViewById(R.id.button_1);
    btn1.setOnClickListener(this);
}

@Override
public void onClick(View v) {
    switch (v.getId()) {
        case R.id.button_1:
            //在此处添加逻辑
            break;
        default:
            break;
    }
}
```

#### 1.3 EditText

允许用户在控件里输入和编辑内容，并可以在程序中对这些内容进行处理

```xml
<EditText
          android:id="@+id/editText"
          android:layout_width="match_parent"
          android:layout_height="wrap_content"
          android:hint="Type something here"
          android:maxLines="2"
          />
```

android:hint  指定一段提示性的文本

android:maxLines  指定了EditText的最大行数



通过点击按钮获取EditText中输入的内容：

调用EditText的 ==getText()== 方法获取输入的内容，再调用toString() 方法将内容转换成字符串

```java
private EditText editText;
private Button btn;

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    editText = (EditText) findViewById(R.id.edit_Text);
    btn = (Button) findViewById(R.id.button_1);
    btn.setOnClickListener(this);
}

@Override
public void onClick(View v) {
    switch (v.getId()) {
        case R.id.button_1:
            String input = editText.getText().toString();
            Toast.makeText(MainActivity.this,input,Toast.LENGTH_SHORT).show();
            break;
        default:
            break;
    }
}
```



#### 1.4 ImageView

