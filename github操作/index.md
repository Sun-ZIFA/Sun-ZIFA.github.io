# GitHub操作


<br/>

>💡 GitHub 官方网址：https://github.com

<br/>

## 创建远程仓库

![](https://blogs-1302550430.cos.ap-guangzhou.myqcloud.com/images/202204021606887.png/webp)

输入仓库名点击创建

![](https://blogs-1302550430.cos.ap-guangzhou.myqcloud.com/images/202204021606888.png/webp)

<br/>

## 远程仓库操作

| 命令名称 | 作用 |
| --- | --- |
| git remote -v | 查看当前所有远程地址别名 |
| git remote add 别名 远程地址 | 起别名 |
| git push 别名 分支 | 推送本地分支上的内容到远程仓库 |
| git clone 远程地址 | 将远程仓库的内容克隆到本地 |
| git pull 远程仓库别名 远程分支名 | 将远程仓库对应分支最新内容拉下来后与当前本地分支直接合并 |

### 创建远程仓库别名

> git remote -v 查看当前所有远程地址别名
> 

> git remote add 别名 远程地址
> 

https://github.com/Sun-ZIFA/Git_Test.git 是创建仓库后的HTTPS地址

```xml
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git remote -v

ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git remote add git-test https://github.com/Sun-ZIFA/Git_Test.git

ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git remote -v
git-test        https://github.com/Sun-ZIFA/Git_Test.git (fetch)
git-test        https://github.com/Sun-ZIFA/Git_Test.git (push)
```

### 推送本地分支到远程库

> git push 别名 分支
> 

```xml
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git push git-test master
Enumerating objects: 13, done.
Counting objects: 100% (13/13), done.
Delta compression using up to 16 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (13/13), 1.03 KiB | 1.03 MiB/s, done.
Total 13 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), done.
To https://github.com/Sun-ZIFA/Git_Test.git
 * [new branch]      master -> master
```

### 克隆远程仓库到本地

> git clone 远程地址
> 

```xml
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/项目备份/ObjectDisk
$ git clone https://github.com/Clover-You/ObjectDisk.git
Cloning into 'ObjectDisk'...
remote: Enumerating objects: 1228, done.
remote: Counting objects: 100% (1228/1228), done.
remote: Compressing objects: 100% (731/731), done.
remote: Total 1228 (delta 766), reused 906 (delta 455), pack-reused 0
Receiving objects: 100% (1228/1228), 1.35 MiB | 718.00 KiB/s, done.
Resolving deltas: 100% (766/766), done.
```

### 拉取远程库内容

> git pull 远程库别名 远程库分支名
> 

```xml
//远程库修改后，将远程仓库对于分支最新内容拉下来后与当前本地分支直接合并
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/Test/Git_Test (master)
$ git pull git-test master
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 686 bytes | 76.00 KiB/s, done.
From https://github.com/Sun-ZIFA/Git_Test
 * branch            master     -> FETCH_HEAD
   cd27077..568ea4b  master     -> git-test/master
Updating cd27077..568ea4b
Fast-forward
 hello.txt | 1 +
 1 file changed, 1 insertion(+)
```
