# 关于android studio中的模拟器被杀死的解决方案(The emulator process for AVD was killed.)

最近两天我的as模拟器一运行就会出现这种报错页面

![image-20210818110851688](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210818110852.png)

在网上搜了几种方案都试过之后，发现仍然无法解决问题：

- 重新安装Android studio

- Android Emulater没有安装

- HAXM需要更新或重新安装

- 将安卓模拟器编辑窗口中的Graphis设置位software

- 将avd剪切放到我们安装sdk的文件夹，修改环境变量ANDROID_SDK_HOME到自己设定的绝对路径下

  

最后自己找出了我电脑为什么模拟器突然会被莫名其妙杀死的原因：==C盘内存不够了==，因为以前经常添加模拟器，又删除不恰当，每个模拟器都有8、9个G，一直堆在C盘里，直到C盘没有内存了我才发现这个问题，解决方法：

找到 c:/user/lenovo/.android/avd文件夹，可以看到那些你删了但没删干净的模拟器

![image-20210818110942080](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210818110943.png)

可以看到每个都非常占用空间，直接delete删除，直到c盘有足够的空间(>=10GB)，足以运行新的模拟器为止

![image-20210818111120645](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210818111225.png)

重新运行avd，成功了

![image-20210818111301130](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210818111302.png)