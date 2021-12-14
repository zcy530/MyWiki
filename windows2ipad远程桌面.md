caiyi 2021/10/03

通过路由器搭建内网穿透隧道

将本台计算机设置为一台服务器

## 一、找到内网ip

进入cmd，输入ipconfig，找到ipv4地址

![image-20211002010749959](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211002010751.png)

接下来配置一下

控制面板，看到程序和功能

![image-20211002005515167](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211002005517.png)

选择启用或关闭 Windows 功能，勾选 Internet Information Services下的 Web管理服务、万维网服务

![image-20211002010034626](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211002010036.png)

打开 管理工具 里的 Internet information Services(IIS)管理器

![image-20211002010349062](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211002010350.png)

点击左边栏，在计算机名文件夹下，网站下已经默认存在一个网站

![image-20211002010502882](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211002010504.png)

选择default web site，点击右边基本设置，可设置网站的目录，我们选择的是本地磁盘的下的一个文件夹，确定

![image-20211002010643035](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211002010644.png)

选择绑定，设置刚才查到的路由器分配给我们的本地IP，端口号为80

![image-20211002011612353](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211002011613.png)

![image-20211002011537034](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211002011538.png)



## 二、找到端口号

打开设置，搜索远程桌面设置

![image-20211003145310219](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211003145311.png)

开启远程桌面设置，并且最好让电脑保持唤醒状态以进行连接

![image-20211003145327865](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211003145329.png)

进入高级设置，可以找到远程桌面端口号

![image-20211003145618377](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211003145619.png)

## 三、在ipad上同一局域网下连接

在app store下载rd client，添加电脑

输入你的 ipv4地址:端口号

连接成功！

## 四、在不同局域网下连接

然后我就把电脑放在宿舍，自信的拿着个平板就出门了，发现连接失败，原来上面的配置只能满足在同一个局域网下连接，现在重点介绍不在同一局域网中怎么连接

**1.ip与mac地址绑定，把路由器分配给被控主机的ip地址设置为静态ip**

右键wifi → 打开网络和internet设置

![image-20211003144519147](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211003144521.png)

更改配适器设置

![image-20211003144742809](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211003144744.png)

点WLAN

![image-20211003144800823](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211003144802.png)

点开详细信息，找到 ipv4 默认网关地址

![image-20211003144817020](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211003144818.png)



打开实验室无线路由器本地IP地址进入路由器设置界面：在浏览器里输入 http://你的ipv4默认网关

进入tp-link管理界面，输入密码，找回密码的方法自行百度

![image-20211002012720178](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211002012725.png)

点击应用管理

![image-20211002012621603](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211002012622.png)

点击Ip与mac地址绑定

![image-20211003145056786](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211003145058.png)

选择你的电脑设备点击加号绑定，这样你的ip地址就固定了



**2.端口映射，把这个静态ip地址映射到3389端口**

即远程桌面连接端口，3389端口开放到互联网上可能会不安全，有需要这可以在Windows注册表中修改远程等的端口号来提高安全性

打开应用管理，虚拟服务器

![image-20211003172148811](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211003172150.png)

添加一个虚拟服务器，ip地址填刚才固定好的静态ip

![image-20211003172243366](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211003172245.png)

**3.设置dmz主机**

主机的ip地址还是刚才的静态ip，把主机的状态改为启用![image-20211003172918349](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211003172919.png)

**4.找到路由器ip**

路由设置 → 上网设置 → 基本设置，里面的ip地址就是路由器ip

![image-20211003173343857](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211003173345.png)

打开rd client，输入路由器ip地址:3389

连接成功！



## 五、突破帧频限制

正常使用没什么问题，只是看视频很卡还掉帧

1.win+R键打开运行窗口，输入regedit，进入注册表编辑器

2.找到并且单击以下的注册表子项HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations

3.右键,点击新建,选择DWORD(32-bit),输入文件名 DWMFRAMEINTERVAL

![image-20211003173655315](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211003173656.png)

右键该文件选择修改,点击十进制,在数值数据中输入15,点击确定

![image-20211003173627352](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211003173628.png)

修改完成后只是理论上能到达60fps,实际上能不能到达该帧率由多方面因素决定,尤其是网络延迟,建议在千兆局域网内进行测试

## 六、解决无法连接到pc的情况

1.确认开启了远程连接，设置好了允许访问的用户

2.确认你是windows专业版，家庭版不支持远程连接

3.ip地址与mac地址没有绑定

我前一天连接成功之后，后一天怎么也连接不上，一直显示“无法连接到远程pc，请保证你的pc已经打开”，猛然发现我的ipv4地址居然跟昨天的不一样了，原来是ip地址没有mac地址绑定，否则会过段时间随机分配一个

4.不在同一局域网下连接不上参考上面的第四步

