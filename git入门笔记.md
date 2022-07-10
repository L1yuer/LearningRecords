# Git学习

Git：分布式版本控制系统

I really `like` *using* **markdown**.

## Git入门概念(持续更新)

### Git Bash

Git Bash是是Windows下的命令行工具，可以执行Linux命令。

### Git CMD

带有 git 命令的常规 Windows 命令提示符。

### Clone

克隆。将远程仓库的代码复制到本地仓库，不管有无权限

### Pull

拉取。拉取远程分支更新到本地仓库，相当于从远程仓库获取最新版本，然后再与本地分支merge（合并）。需要仓库权限

### Push

推送。将本地仓库代码上传到远程仓库。

## Git入门操作(持续更新)

### git init

初始化一个git仓库，使其能够被git管理

### git add

添加一个或多个文件到暂存区：

```shell
git add [file1] [file2] ...
```

添加指定目录到暂存区，包括子目录：

```shell
git add [dir]
```

添加当前目录下的所有文件到暂存区：

```shell
git add .
```

执行 **git status**，就可以看到这暂存区里的文件状态：

A：已经添加

AM：添加到暂存区之后又有改动

### git commit

将暂存区内容添加到本地仓库中:

```shell
git commit -m [message]
```

提交暂存区的指定文件到仓库区：

```shell
git commit [file1] [file2] ... -m [message]
```

### git branch

创建一个分支

```shell
git branch <branch name>
```

列出分支

```shell
git branch
```

### git fetch

`git fetch`将远程主机的最新内容拉到本地，用户在检查了以后决定是否合并到工作本机分支中。

`git pull`  则是将远程主机的最新内容拉下来后直接合并。

区别如图所示

![](http://kmknkk.oss-cn-beijing.aliyuncs.com/image/git.jpg)
