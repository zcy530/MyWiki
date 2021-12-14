

# springboot项目部署到windows服务器

### 一、将项目打包成war包，在maven中clean，package，然后找到war包地址

![image-20210911102615905](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210918001358.png)

### 二、购买阿里云服务器

此处白嫖了一个两周的高校计划服务器，记住公网ip，以后将用这个ip访问网页

![image-20210912141319280](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210918001402.png)

### 三、在本地远程连接到服务器

![image-20210912141517830](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210912141519.png)

可以设置共享d盘资源

![image-20210912145836344](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210912145838.png)

在弹出来的密码框里输入密码，并且信任该远程计算机

![image-20210912141640552](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210912141642.png)

### 四、给服务器配置jdk

这里以jdk11为例，最好在选择版本的时候选jdk1.8！因为要和tomcat版本相对应，我当时都是把jdk11卸载了重新安装的jdk1.8

1. 搜索jdk，进入Oracle官网

   ![image-20210521121334351](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521121334351.png)

2. 点击JDK download

   ![image-20210521121518531](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521121518531.png)

3. 选择合适的版本和位数，此处以JDK11，win10，x64为例

   ![image-20210521122000743](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521122000743.png)

4. 下载完成后打开exe

   <img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521124037196.png" alt="image-20210521124037196" style="zoom:67%;" />

5. 打开cmd，输入java -version查看是否安装成功

   ![image-20210521124326205](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521124326205.png)

6. 这是安装好的场景，如果没有，可能需要配置环境变量

   此电脑–>属性->高级系统设置->环境变量->编辑

   添加好jdk的bin目录之后，一路点确认

   ![image-20210521124637474](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/image-20210521124637474.png)

### 五、配置Tomcat

用于将我们的项目发布到外网，然后我们就可以使用之前的外网ip访问我们的远程服务器了

首先，进入官网，选择好版本。注意！！jdk版本和tomcat版本一定要对应，比如pom.xml规定了java version是1.8，则对应tomcat8，如果java version是1.9，则对应tomcat9

![image-20210917160957439](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210917160959.png)

![image-20210917161039369](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210917161041.png)

直接把zip文件在文件夹里解压就好

![image-20210917161137355](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210917161139.png)

在环境变量里配置一下 JAVA_HOME 和 CATALINA_HOME，分别对应jdk和tomcat下载目录

![image-20210917161401365](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210917161403.png)

### 六、安装mysql和navicat

一定要注意密码！

服务器上mysql的密码一定要和项目里面配置的账号密码一致，我就是这里没配好，导致一直运行项目时数据库连接报错，还有就是一定要认真看报错信息，我每次运行都是页面404，一直没看报错信息，最后才发现是数据库密码不对的问题

安装好mysql和navicat，可以将我们的导出的blog.sql文件导入，看能不能连接

方法：新建数据库 → 运行SQL文件

![image-20210918000518644](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210918000521.png)

![image-20210918000629305](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210918000631.png)

### 七、启动Tomcat

把我们之前准备好的blog.war文件复制到服务器中，再复制到 apache-tomcat-8.5.70 → webapps 目录下面

![image-20210917235853053](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210917235855.png)

打开 apache-tomcat-8.5.70 → bin → startup.bat，启动tomcat

![image-20210918000006182](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210918000008.png)

要是成功的话，应该可以在服务器的 http://localhost:8080/blog/ 访问到你部署的网页了

![image-20210918000141446](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210918000144.png)

### 八、一些踩坑记录！

很难相信我整整部署了三天才成功，感觉把全网的有的没的坑都踩了一遍，就是尝试了网上说的各种解决方案，每次启动tomcat后访问blog页面都还是404，每次都是everytime！最后一天差点要放弃了，真的真的马上就要放弃了，可就在我万念俱灰的时候突然成功了，于是决定一定要把这个过程记录下来，虽艰辛但确实学到了很多

#### 问题1

如果访问正常路径404了

![image-20210913201128807](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210913201128807.png)

解决：修改启动类BlogApplication，继承SpringBootServletInitializer，然后重写configure方法

```java
@SpringBootApplication
public class BlogApplication extends SpringBootServletInitializer {
	@Override
	protected SpringApplicationBuilder configure(SpringApplicationBuilder builder) {
		return super.configure(builder);
	}
	public static void main(String[] args) {
		SpringApplication.run(BlogApplication.class, args);
	}
}
```

pom.xml文件中加入servlet依赖

```xml
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <scope>provided</scope>
</dependency>
```

#### 问题2

运行项目连接Mysql时出现警告：Establishing SSL connection without server's identity verification is not recommende

解决：在url里面添加useSSL=false

![image-20210917234411993](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210917234413.png)



#### 问题3

服务器部署web项目服务器可以访问，外网访问不了

在你的阿里云服务器找到你的实例列表，更多 → 网络安全组 → 安全组配置

![image-20210917162310983](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210917162312.png)

自定义加入8080端口

![image-20210917162440747](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210917162442.png)



#### 问题4

如果本地sql和服务器sql

我是来自华东师范大学软件工程大三的张彩仪，我语言能力强、综合素质高、热心公共事务、富有爱心，具有很好的与人沟通的能力、跨文化交际与理解能力。大一大二时担任学生会部长和团支书的经历让我快速适应了高强度的工作氛围，服务学校服务学生，希望可以给服务人类命运共同体提供经验和借鉴，也希望学习一些国际上成熟的项目运营和组织管理经验。

我非常关心各种社会话题，特别是性别平等人权方面，我曾阅读过许多资料和书籍，参与过平权组织的志愿者活动。作为软件工程的学生，同时非常关注科技与社会的关系，我也参与过中国开源大会COSCon等全球技术交流活动的志愿者。我坚信一些国际性问题必须由各国的专业化人才通过国际组织的平台来协商解决，国际治理的舞台也需要更多来自中国的人才来参与。希望能在此学习、工作，在全新的场景中认识世界



华东师范大学优秀共青团干部，优秀学生骨干，华东师范大学二等奖学金，“互联网+”全国大学生创新创业大赛校级一等奖，“挑战杯”全国大学生课外学术科技作品竞赛三等奖，创新创业大赛国家级评定，上海苗苗阅读公益项目优秀志愿者