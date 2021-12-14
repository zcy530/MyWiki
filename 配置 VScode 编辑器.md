# 配置 VScode 编辑器 (前端篇)

2021/8/2



## 一、代码片段设置

左下角设置 -> 用户代码片段

![image-20210802223434589](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210803143108.png)

上面弹框输入 HTML，或者JavaScript，css，以html举例

![image-20210802223522095](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210802223523.png)

在弹出的 html.json 文件里可以写自己想要配置的代码块，例如：

![image-20210802231441466](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210802231442.png)

上面的内容表示，在编辑器输入"prefix" 的内容之后就会自动跳出 "body" 段的代码，"$" 符号表示光标指向的地方，效果如下：

![image-20210803125536685](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210803143121.png)

输入dul回车，就会自动弹出 "body" 预置好的代码，非常方便

![image-20210803125601356](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210803125603.png)



## 二、常用插件

### 1. open in browser

作用：html页面在浏览器中打开预览

点击左侧栏的第五个方块图标，搜索 open in browser 插件，点击安装

![image-20210802225015519](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210802225018.png)

此时再打开html页面，右键单击，就有了 open in default browser 的选项，选择打开默认浏览器

![image-20210802225055036](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210802225056.png)

也可以点击 open in other browser 选择其他浏览器

![image-20210802225235763](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210802225237.png)

success！

![image-20210803132810444](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210803132812.png)

### 2. Guides

作用：辅助线对齐，选中的代码块会通过红线匹配前缀后缀，以免代码繁多搞砸

![image-20210803131234599](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210803131235.png)

效果：

![image-20210803131345716](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210803131346.png)



### 3. HTMLHint

作用：html代码检测，支持html5，错误的地方会标下滑波浪线，提示错误信息

![image-20210803131702423](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210803131703.png)



### 4. Path Intellisense

作用：可以很好的识别引入文件的路径，根据路径提示功能

![image-20210803132534889](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210803132536.png)

效果如下图：

![image-20210803132705043](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210803132706.png)



### 5. Material Theme

作用：这是一款颜色主题的插件，让你的编辑器变得更顺眼

![image-20210803133425285](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210803133426.png)

安装完成后，左下角设置，颜色主题

![image-20210803133601675](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210803133603.png)

在上方弹出的选项框里选择你喜欢的主题，我个人喜欢 ocean 的蓝色！

![image-20210803133622388](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210803133624.png)



### 6. prettier

作用：在保存的时候格式化代码，让代码整洁易懂

![image-20210803134032298](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210803134033.png)

安装成功后，在左下角 设置 -> 设置 -> 输入save ->勾选 Format On Save

![image-20210803134236423](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210803134238.png)

点shift + alt +F 第一次格式化，会弹出一个选框配置格式化插件，选择 prettier

当每次保存html文件时就可以自动格式化了



### 7. vetur

作用：vue多功能集成插件，包括语法高亮，智能提示，emmet，错误提示，格式化

![image-20210803132302492](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210803132303.png)



### 8. carbon-now-sh

作用：将代码段生成一张图片

![image-20210803134710579](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210803134711.png)

安装后，选择要展示的代码，按F1 或者 ctrl + shift + p 在上方输入框输入 carbon，然后回车

![image-20210803135101756](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210803143122.png)

此时会弹出一个网页（需要稳定网络），里面是代码截图，点击export可以导出截图

![image-20210803135404767](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210803143123.png)



### 9.Auto Rename Tag

作用：修改html标签，自动完成头部和尾部闭合标签的同步修改

![image-20210803141113160](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210803141116.png)



### 10. Project-tree

作用：自动生成项目目录文件结构树，并写入readme中

使用：Shift + Cmd + p  —> 输入：Project Tree  —>  找到需要生成目录的项目  —>  回车

![image-20210813120425330](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210813120427.png)

![image-20210813145308004](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210813145309.png)



## 三、常用快捷键

```
新建文件:   Ctrl+N
文件之间切换:   Ctrl+Tab
代码行向左或向右缩进:   Ctrl+[ 、 Ctrl+]
代码格式化:   Shift+Alt+F
向上或向下移动一行:   Alt+Up 或 Alt+Down
向上或向下复制一行:   Shift+Alt+Up 或 Shift+Alt+Down
移动到行首:   Home(fn + ←)
移动到行尾:   End(fn + →)
移动到文件结尾:   Ctrl+End
移动到文件开头:   Ctrl+Home
多行编辑(列编辑):   Alt+Shift+鼠标左键 或 Ctrl+Alt+Down/Up
手动保存:   Ctrl+S
全屏显示(再次按则恢复):   F11
放大或缩小(以编辑器左上角为基准):   Ctrl +/-
```

未完待续......目前是初学前端阶段，在今后开发过程中遇到好用的插件还会继续更新、整理

