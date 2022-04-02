# Git分支操作


<br/>

## 什么是分支

在版本控制过程中，同时推进多个任务，为每个任务，我们就可以创建每个任务的单独分支。使用分支意味着程序员可以把自己的工作从开发主线上分离开来，开发自己分支的时候，不会影响主线分支的运行。对于初学者而言，分支可以简单理解为副本，一个分支就是一个单独的副本。（分支底层其实也是指针的引用）

<br/>

## 分支的好处

同时并行推进多个功能开发，提高开发效率。

各个分支在开发过程中，如果某一个分支开发失败，不会对其他分支有任何影响。失败的分支删除重新开始即可。

<br/>

## 分支的操作

| 命令名称 | 作用 |
| --- | --- |
| git branch 分支名 | 创建分支 |
| git branch -v | 查看分支 |
| git checkout 分支名 | 切换分支 |
| git merge 分支名 | 把指定的分支合并到当前分支上 |

### 查看分支

> git branch -v

```xml
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git branch -v
* master a6fa5e1 first commit （*代表当前所在的分区）
```

### 创建分支

> git branch 分支名

```xml
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git branch hot-fix

ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git branch -v
  hot-fix a6fa5e1 first commit
* master  a6fa5e1 first commit
```

### 切换分支

> git checkout 分支名

```xml
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git checkout hot-fix
Switched to branch 'hot-fix'

ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (hot-fix)
$
```

### 合并分支

> git merge 分支名

```xml
//切换到hot-fix分支
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git checkout hot-fix
Switched to branch 'hot-fix'

//修改hot-fix分支下的hello.txt Welcome to you
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (hot-fix)
$ vim hello.txt

//添加到暂存区
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (hot-fix)
$ git add hello.txt

//提交到本地库
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (hot-fix)
$ git commit -m "hot-fix first commit" hello.txt
[hot-fix 7aab108] hot-fix first commit
 1 file changed, 1 insertion(+), 1 deletion(-)

//切换到主分区master
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (hot-fix)
$ git checkout master
Switched to branch 'master'

//在主分区master下合并hot-fix分区
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git merge hot-fix
Updating a6fa5e1..7aab108
Fast-forward
 hello.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)

//查看hello.txt文件 已经修改
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ cat hello.txt
Hello World! Welcome to you!
```

### 产生冲突

冲突产生的表现：后面状态为 MERGING

```xml
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master|MERGING)
```

冲突产生的原因：

合并分支时，两个分支在同一个文件的同一个位置有两套完全不同的修改。Git 无法替
我们决定使用哪一个。必须人为决定新代码内容。

```xml
//修改master分支上的hello.txt 添加一行Hello WPF！
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ vim hello.txt

//添加到暂存区
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git add hello.txt

//提交到本地库
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git commit -m "update 1" hello.txt
[master 4e3f85c] update 1
 1 file changed, 1 insertion(+)

//切换到hot-fix分区
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git checkout hot-fix
Switched to branch 'hot-fix'

//修改hot-fix分区的hello.txt 添加一行Hello Git！
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (hot-fix)
$ vim hello.txt

//添加到暂存区
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (hot-fix)
$ git add hello.txt

//提交到本地库
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (hot-fix)
$ git commit -m "update 2"
[hot-fix fc47191] update 2
 1 file changed, 1 insertion(+)

//切换到master主分区
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (hot-fix)
$ git checkout master
Switched to branch 'master'

//合并hot-fix分区，提示需要手动合并代码 后面状态为MERGING
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git merge hot-fix
Auto-merging hello.txt
CONFLICT (content): Merge conflict in hello.txt
Automatic merge failed; fix conflicts and then commit the result.

//编辑有冲突的文件hello.txt，删除特殊符号，保留要使用的内容
//特殊符号：<<<<<<< HEAD 当前分支的代码 ======= 合并过来的代码 >>>>>>> hot-fix
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master|MERGING)
$ vim hello.txt

//添加到暂存区
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master|MERGING)
$ git add hello.txt

//提交到本地库时不能带文件名，不然报错
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master|MERGING)
$ git commit -m "update 3" hello.txt
fatal: cannot do a partial commit during a merge.

//提交到本地库
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master|MERGING)
$ git commit -m "update 3"
[master cd27077] update 3

//发现后面MERGING消失，变为正常
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$
```
