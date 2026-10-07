# GIT

## 一、GIT的安装

第一步：下载

```
官网：https://git-scm.com/
```

第二步：双击exe,看不懂就无脑下一步



## 二、基本使用

1.配置用户和邮箱

```
git config --global user.name “ukazuha”
git config --global user.email "952391175@qq.com"

检查是否成功
git config --global --list
```

2.基本状态：git status

```
Git的本质是对版本进行控制，也就是对文件的版本进行控制，使用Git对文件进行修改、或者提交等操作时，需要知道文件当前处于什么状态，不然可能会出现提交了现在不想提交的文件，或者要提交的文件却没有提交上，在Git中文件分为以下状态：
"Untracked"：文件未跟踪；此文件在文件夹中，但并没有加入git库，不参与版本控制。
"Unmodify"：文件已入库，并且未修改；即版本库中的文件内容与文件夹中完全一致。
"Modified"：文件已修改；仅仅是修改，并没有进行其它操作。
"Staged"：文件已暂存；并没有同步到本地版本库中。
"Committed"：文件已提交；已提交到本地版本库，受到版本控制。
```

3.初始化本地仓库：即创建文件夹，然后git bash here

```
git init
这个操作会让文件夹多一个.git文件夹
```

4.将文件放到暂存区

```
git add 文件名
git add .
```

5.将暂存区内的文件提交到库区

```
git commit -m "备注信息"
```

## 三、使用前的准备

### 3.1 设置SSH-KEY

* 生成密钥

```
ssh -keygen -t rsa -C
一路回车
```

* github添加密钥，验证连接

```
ssh -T git@github.com
```



### 3.2  建立远端仓库与本地仓库的连接

1.远端仓库初始化方式

在远端建立仓库初始化后，再克隆到本地，后面进行push和pull



2.本地初始化方式

本地初始化一个仓库

# 正式学习

## 四、通过实际操作来学习Git

### 4.1 基本操作

* 初始化仓库

```
git init
```

* 查看仓库状态

```
git status
```

* 向暂存区添加文件

```
git add 文件名
git add .		--所有文件
```

* 保存仓库的历史纪录

```
git commit [-m] "说明信息"
```

* 产看提交日志

```
git log

--pretty=short	一行简述信息

git log 文件名，只查看这个文件的提交信息

-p		显示文件
```



