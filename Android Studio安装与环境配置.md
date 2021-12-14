## Android Studio安装与环境配置

Caiyi  2021/5/21

首先了解安卓开发需要的工具

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200516095553968.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzM3MTQ5MDYy,size_16,color_FFFFFF,t_70)

#### 一、安装JDK

1. 搜索jdk，进入Oracle官网

   ![image-20210521121334351](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521121334351.png)

2. 点击JDK download

   ![image-20210521121518531](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521121518531.png)

3. 选择合适的版本和位数，此处以JDK11，win10，x64为例

   ![image-20210521122000743](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521122000743.png)

4. 下载完成后打开exe

   <img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521124037196.png" alt="image-20210521124037196" style="zoom:67%;" />

      <img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521124157539.png" alt="image-20210521124157539" style="zoom:67%;" />

5. 打开cmd，输入java -version查看是否安装成功

   ![image-20210521124326205](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521124326205.png)

6. 这是安装好的场景，如果没有，可能需要配置环境变量

   此电脑–>属性->高级系统设置->环境变量->编辑

   添加好jdk的bin目录之后，一路点确认

   ![image-20210521124637474](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521124637474.png)

   

#### 二、Android Studio的安装

1. 进入Android官网https://developer.android.google.cn/studio/选择适合的版本进行download

   ![image-20210521122142964](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521122142964.png)

2. 双击下载的文件，进入安装界面，点击“next”进入下一步

   ![img](https://pic1.zhimg.com/80/v2-0ae70036f6812b7bacc433e7efc0b59c_1440w.jpg)

3. 一直点next直到安装成功，finish

   ![img](https://pic4.zhimg.com/80/v2-881b97e059c9ae45f94926850b58d1b7_1440w.jpg)

   

4. 在第一次运行时，若出现Unable to access Android SDK add-on list，表示Android Studio找不到Sdk，点击cancel 即可，没有什么大碍，等装好SDK后，自然就好了，下一步将会介绍如何安装SDK

   如果非常介意这个窗口，可以在 Android Studio 安装目录 bin/idea.properties 文件最后追加一句disable.android.first.run=true

   ![image-20210521122326928](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521122326928.png)



#### 三、Android SDK的安装

1. 在欢迎页点击Configure-SDK Manager

   或者在新建项目打开File-Settings-Appearance&Behavior-System Settings-Android SDK

   ![image-20210521122913585](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521122913585.png)

2. 点击SDK Update sites勾选Force https://..

   ![image-20210521123035164](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521123035164.png)

3. 点击SDK Platforms，勾选Android10.0(Q)，点Apply，等待自动安装完成

   ![image-20210521123101909](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521123101909.png)



#### 四、AVD配置（虚拟机）

1. 在欢迎页点击Configure-AVD Manager

   ![image-20210521122913585](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521122913585.png)

2. 选择普通电脑比较带的动的pixel2或者nexus S

   ![image-20210521125919662](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521125919662.png)

3. 点击第一个download，等待安装

   ![image-20210521130007996](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521130007996.png)

   ![image-20210521130104241](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521130104241.png)

4. 安装完成之后，点击上方的运行按钮，然后就可以运行你的第一个项目啦

   ![image-20210521130625812](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521130625812.png)