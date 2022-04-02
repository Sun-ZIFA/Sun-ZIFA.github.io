# Git常用命令


| 命令名称 | 作用 |
| --- | --- |
| git config -- global user.name 用户名 | 设置用户签名 |
| git config -- global user.email 邮箱 | 设置用户签名 |
| git init | 初始化本地库 |
| git status | 查看本地库状态 |
| git add 文件名 | 添加到暂存区 |
| git commit -m “日志信息” 文件名 | 提交到本地库 |
| git reflog | 查看历史记录 |
| git reset -- hard 版本号 | 版本穿梭 |

<br/>

## 设置用户签名

签名的作用是区分不同操作者身份。用户的签名信息在每一个版本的提交信息中能够看到，以此确认本次提交是谁做的。Git 首次安装必须设置一下用户签名，否则无法提交代码。

这里设置用户签名和将来登录 GitHub（或其他代码托管中心）的账号没有任何关系。

> git config --global user.name 用户名
>
> git config --global user.email 邮箱

```xml
ZIFA@LAPTOP-OU8IUASF MINGW64 ~
$ git config --global user.name ZIFA
ZIFA@LAPTOP-OU8IUASF MINGW64 ~
$ git config --global user.email 1697838602@qq.com
```

<br/>

## 初始化本地库

> git init

```xml
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test
$ git init
Initialized empty Git repository in E:/Test/Git_Test/.git/
```

初始化会在项目地址生成.git文件夹，需要显示隐藏文件

<br/>

## 查看本地库状态

> git status

首次查看 工作区没有任何文件

```xml
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

新增hello.txt文件

```xml
//内容：Hello World！
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ vim hello.txt
```

再次查看 检测到未追踪的文件

```xml
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        hello.txt

nothing added to commit but untracked files present (use "git add" to track)
```

<br/>

## 添加暂存区

> git add 文件名

```xml
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git add hello.txt
warning: LF will be replaced by CRLF in hello.txt.
The file will have its original line endings in your working directory
```

查看状态 检测到暂存区有新文件

```xml
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   hello.txt
```

<br/>

## 提交到本地库

> git commit -m “日志信息” 文件名

```xml
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git commit -m "first commit" hello.txt
warning: LF will be replaced by CRLF in hello.txt.
The file will have its original line endings in your working directory
[master (root-commit) a6fa5e1] first commit
 1 file changed, 1 insertion(+)
 create mode 100644 hello.txt
```

查看状态 没有文件需要提交

```xml
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git status
On branch master
nothing to commit, working tree clean
```

<br/>

## 修改文件

```xml
//修改hello.txt里面的内容 另添加一行Hello Git！
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ vim hello.txt

//查看状态 检测到工作区有文件被修改
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   hello.txt

no changes added to commit (use "git add" and/or "git commit -a")

//将修改的文件再次添加到暂存区
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git add hello.txt
warning: LF will be replaced by CRLF in hello.txt.
The file will have its original line endings in your working directory

//查看状态 工作区的修改添加到了暂存区
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   hello.txt

//提交到本地库
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git commit -m "second commit" hello.txt
warning: LF will be replaced by CRLF in hello.txt.
The file will have its original line endings in your working directory
[master 6935bb4] second commit
 1 file changed, 1 insertion(+)

//查看状态
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git status
On branch master
nothing to commit, working tree clean
```

<br/>

## 历史版本

### 查看历史版本

> git reflog 查看版本信息
> git log 查看版本详细信息

```xml
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git reflog
6935bb4 (HEAD -> master) HEAD@{0}: commit: second commit
a6fa5e1 HEAD@{1}: commit (initial): first commit

ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git log
commit 6935bb458799fafc90d83a30345dc154f634ef16 (HEAD -> master)
Author: liuzifa <1697838602@qq.com>
Date:   Wed Mar 30 10:00:11 2022 +0800

    second commit

commit a6fa5e1bd1b3bc5f757cf434241868b80622d0dc
Author: liuzifa <1697838602@qq.com>
Date:   Wed Mar 30 09:19:37 2022 +0800

    first commit
```

### 版本穿梭

> git reset --hard 版本号

```xml
//首先查看当前的历史记录，可以看到当前是在 6935bb4 这个版本
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git reflog
6935bb4 (HEAD -> master) HEAD@{0}: commit: second commit
a6fa5e1 HEAD@{1}: commit (initial): first commit

//切换到 a6fa5e1 版本，也就是我们第一次提交的版本
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git reset --hard a6fa5e1
HEAD is now at a6fa5e1 first commit

//切换完毕之后再查看历史记录，当前成功切换到了 a6fa5e1 版本
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git reflog
a6fa5e1 (HEAD -> master) HEAD@{0}: reset: moving to a6fa5e1
6935bb4 HEAD@{1}: commit: second commit
a6fa5e1 (HEAD -> master) HEAD@{2}: commit (initial): first commit

//然后查看文件 hello.txt，发现文件内容已经变化
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ cat hello.txt
Hello World!
```
