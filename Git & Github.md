# Git & Github 使用笔记

2021/8/7

## 一、安装git

设置用户名密码



## 二、创建远程仓库

在 github 里创建一个新的仓库，以 test_repository 为例

![image-20210812230142475](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812233931.png)



在创建完仓库后，复制它的远程仓库地址，这里使用 HTTP 地址

![image-20210812235120640](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812235122.png)



## 三、将本地仓库推到远程

### 1. 认识文件的四种状态

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812233924.PNG" alt="IMG_7017" style="zoom: 67%;" />

### 2. 如果没有本地仓库

```
# 创建本地仓库
git init

# 将单个文件添加到暂存区
git add filename

# 将所有文件添加到暂存区
git add .

# 提交历史记录
git commit -m "info"

# 查看日志
git log

# 查看所有的操作记录
git reflog
```



实际操作如下：

在你想上传的文件夹中空白处右键 -> git bash here

![image-20210812220002383](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812220003.png)



在命令行中输入 *git init* 就会看到文件夹当中生成了一个 *.git* 的隐藏文件，它所在的文件夹就是仓库，它会记录你所有的变更行为

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812220022.png" alt="image-20210812215555747" style="zoom: 80%;" />



接下来我们尝试创建两个文件 *index.html 和 index.js*，在命令行中输入 *git status* 可以查看当前仓库的状态信息

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812215934.png" alt="image-20210812215932754" style="zoom:67%;" />



我们用 *git add index.html* 命令把单个文件 *index.html* 加到缓存区里

再用  *git status* 查看当前仓库的状态信息，发现 *index.html* 已经绿了

如果想把项目里所有的文件都上传到缓存区，可以用 *git add .* 来实现

<img src="https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812220735.png" alt="image-20210812220619365" style="zoom:67%;" />



![image-20210812221123317](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812221125.png)



接下来就可以提交这次变更了 -m 是 message 的意思，后面跟上跟此次变更信息有关的描述

在提交后通过 *git log* 查看日志，通过日志我们可以查看什么人在什么时间，提交了一个什么样的commit

![image-20210812221523888](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812233909.png)



### 3. 如果已有本地仓库

```
# 添加远端仓库地址
git remote add origin(给远程仓库地址起的别名) 你的远程仓库地址

# 推送提交
git push -u origin(远程仓库) master(分支信息)
```



**实际演示：**

*git remote add origin* 把远程仓库地址保存起来，表示以后就可以用 origin 代替你这一长串的远程仓库地址

![image-20210812235519280](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812235521.png)



*git push -u origin  master* 将本地仓库推向远程仓库，如果网络不好可能会失败

成功后会弹出一个GitHub的登录框， 输入邮箱和密码

![image-20210813092630146](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210813092633.png)

上传成功！可以在你的GitHub远程仓库看到我们在本地添加的 *index.html 和 index.js* 文件了

![image-20210813093638530](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210813093640.png)

![image-20210813093739604](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210813093900.png)

## 四、项目代码变动提交

```
git add 文件
git commit -m "提交日志"

# 取消我的commit
git reset commitID --hard
git reset commitID --soft
git reset commitID --mixed

# 如果修改了提交信息，则重新
git push -u 远程仓库名 分支信息
```

**reset --hard/soft/mixed三个参数对比：**

hard：在本地库移动 HEAD 指针，也会重置暂存区，也会重置工作区

soft：仅仅是在本地库移动 HEAD 指针

mixed：在本地库移动 HEAD 指针，也会重置暂存区

**实际演示：**

我们修改一下index.js文件几行代码之后再查看状态，会发现又出现了红色的文件，红色的文件代表有新的变更

![image-20210812221802905](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812233904.png)



我们需要重复以上的操作，先用 git add . 将所有文件提交到暂存区，再提交 *git commit -m* ，通过 *git log* 可以看到的确已经提交了

![image-20210812222233112](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812233900.png)



如果想要取消一个commit，恢复到 first commit 的版本，就在 git log 里找到第一次的 commitID

![image-20210812225551499](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812233856.png)



如果想要取消一个commit，恢复到 first commit 的版本，也可以在 *git reflog* 里面找到一个短的索引值，这样引用比较方便

![image-20210812232740460](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812233852.png)

