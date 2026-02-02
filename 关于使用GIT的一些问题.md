# 1.实际操作

## 1.1 基本操作

```
git init   初始化为仓库
git status 查看仓库的状态
git add 向暂存区添加文件
git commit 保存仓库的历史记录
```

```
git log 产看提交日志
git log --pretty=short 只显示提交信息的第一行
git log README.md 只显示指定文件、目录的日志
git log -p 显示文件的改动
git diff 查看更改前后的差别
```

## 1.2 分支操作

```
git branch 显示分支一览表
git checkout -b 创建、切换分支
git checkout - 切换回上一个分支
git merge 合并分支          git merge --no-ff feature-A
git log --graph 以图表的方式查看分支
```

## 1.3 更改提交的操作

```
git reset 回溯历史版本
```





# 2.本地仓库与远端仓库连接

## 1.1 仓库在远端初始化

```
在远端建立一个仓库初始化后，可直接在本地git bash界面，通过输入：
git clone 克隆地址(git@github.com:uKazuha/Code.git)
```



## 1.2 仓库在本地初始化

```
本地git init初始化仓库后，在远端也创建一个仓库，注意，远端创建仓库时，不要勾选创建README.txt文件
```

```
准备工作完成后，通过git remote add添加远程仓库
git remote add origin git@github.com:uKazuha/Note.git
以上命令将该远端仓库命名为origin（标识符）

接下来推送操作：
git push -u origin main
推送到origin远端的main分支
```

