# GitHubæä½


<br/>

>ð¡ GitHub å®æ¹ç½åï¼https://github.com

<br/>

## åå»ºè¿ç¨ä»åº

![](https://blogs-1302550430.cos.ap-guangzhou.myqcloud.com/images/202204021606887.png/webp)

è¾å¥ä»åºåç¹å»åå»º

![](https://blogs-1302550430.cos.ap-guangzhou.myqcloud.com/images/202204021606888.png/webp)

<br/>

## è¿ç¨ä»åºæä½

| å½ä»¤åç§° | ä½ç¨ |
| --- | --- |
| git remote -v | æ¥çå½åææè¿ç¨å°åå«å |
| git remote add å«å è¿ç¨å°å | èµ·å«å |
| git push å«å åæ¯ | æ¨éæ¬å°åæ¯ä¸çåå®¹å°è¿ç¨ä»åº |
| git clone è¿ç¨å°å | å°è¿ç¨ä»åºçåå®¹åéå°æ¬å° |
| git pull è¿ç¨ä»åºå«å è¿ç¨åæ¯å | å°è¿ç¨ä»åºå¯¹åºåæ¯ææ°åå®¹æä¸æ¥åä¸å½åæ¬å°åæ¯ç´æ¥åå¹¶ |

### åå»ºè¿ç¨ä»åºå«å

> git remote -v æ¥çå½åææè¿ç¨å°åå«å
> 

> git remote add å«å è¿ç¨å°å
> 

https://github.com/Sun-ZIFA/Git_Test.git æ¯åå»ºä»åºåçHTTPSå°å

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

### æ¨éæ¬å°åæ¯å°è¿ç¨åº

> git push å«å åæ¯
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

### åéè¿ç¨ä»åºå°æ¬å°

> git clone è¿ç¨å°å
> 

```xml
ZIFA@LAPTOP-OU8IUASF MINGW64 /e/é¡¹ç®å¤ä»½/ObjectDisk
$ git clone https://github.com/Clover-You/ObjectDisk.git
Cloning into 'ObjectDisk'...
remote: Enumerating objects: 1228, done.
remote: Counting objects: 100% (1228/1228), done.
remote: Compressing objects: 100% (731/731), done.
remote: Total 1228 (delta 766), reused 906 (delta 455), pack-reused 0
Receiving objects: 100% (1228/1228), 1.35 MiB | 718.00 KiB/s, done.
Resolving deltas: 100% (766/766), done.
```

### æåè¿ç¨åºåå®¹

> git pull è¿ç¨åºå«å è¿ç¨åºåæ¯å
> 

```xml
//è¿ç¨åºä¿®æ¹åï¼å°è¿ç¨ä»åºå¯¹äºåæ¯ææ°åå®¹æä¸æ¥åä¸å½åæ¬å°åæ¯ç´æ¥åå¹¶
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
