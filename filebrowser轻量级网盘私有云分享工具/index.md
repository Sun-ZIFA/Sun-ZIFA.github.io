# FileBrowser轻量级网盘（私有云）分享工具


<br/>

因为分享自己的js等文件十分不方便，所以就想搭建一个自己的个人分享云盘，可以随时随地上传小文件，无限制下载，经过筛选，最终决定使用FileBrowser来搭建自己的私有云盘分享工具，只需要一个云服务器。

FileBrowser官网地址：https://github.com/filebrowser/filebrowser

<br/>


## 服务器配置

建议在有活动的时候购买服务器，常见的服务器：[腾讯云](https://curl.qcloud.com/BCHO4DcO)，[阿里云](https://www.aliyun.com/activity/new?userCode=cfziz7jb)，购买地址带了我的返佣链接，如果介意直接百度去官网买就好了哈。

服务器配置看个人需求吧,根据预设来选择，购买时会让你选择系统，建议Centos7

可以使用SSH工具进行远程服务器，推荐finallshell和xshell，可以去官网下载安装

<br/>

## 宝塔安装

去[宝塔官网](https://www.bt.cn/new/index.html)安装，选择Linux面板，现在适合自己服务器系统的命令，复制命令到ssh安装

我这里使用的是centos7安装命令

```
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh
```

![](https://blogs-1302550430.cos.ap-guangzhou.myqcloud.com/images/202204110838613.png/webp)

安装完成后去服务器控制台放行8888端口

登录宝塔外网地址，用安装时生成的账号密码登录，可以一键安装宝塔推荐的一些LNMP

<br/>

## 安装Docker

> 万物皆可Docker

装完宝塔再安装Docker就超级简单，宝塔面板点击软件商店，搜索docker然后安装

![](https://blogs-1302550430.cos.ap-guangzhou.myqcloud.com/images/202204110838614.png/webp)



> 国内拉取镜像可能特别慢，可以配置一些镜像加速器，这样提高下载速率

宝塔面板👉软件商店👉Docker设置👉加速器👉复制下面内容👉保存

```
{"registry-mirrors": ["https://docker.mirrors.ustc.edu.cn", "https://hub-mirror.c.163.com", "https://mirror.baidubce.com", "https://reg-mirror.qiniu.com"]}
```



四个分别是科大镜像、网易镜像、百度镜像、七牛云镜像

![](https://blogs-1302550430.cos.ap-guangzhou.myqcloud.com/images/202204110838615.png/webp)

<br/>

## 安装FileBrowser

宝塔面板点击文件，创建两个文件夹filebrowser和yalida（可以自定义名字），filebrowser是数据文件，yalida是分享文件存放目录

![](https://blogs-1302550430.cos.ap-guangzhou.myqcloud.com/images/202204110838616.png/webp)

<br/>

filebrowser文件夹下再创建config和database文件夹，config下创建配置文件settings.json，database下创建数据库文件filebrowser.db，目录树如下：

```
├── filebrowser
│   ├── config
│   │   └── settings.json
│   └── database
│       └── filebrowser.db
├── yalida
```

<br/>

双击编辑settings.json文件，输入以下内容并保存

```json
{
  "port": 80,
  "baseURL": "",
  "address": "",
  "log": "stdout",
  "database": "/database/filebrowser.db",
  "root": "/srv"
}
```

<br/>

然后一键安装FileBrowser，ssh工具中输入以下命令（需要一行一行输入！！！）

```
sudo docker run -d \
    -v /www/wwwroot/yalida:/srv \  
    -v /www/wwwroot/filebrowser/database/filebrowser.db:/database/filebrowser.db \
    -v /www/wwwroot/filebrowser/config/settings.json:/config/settings.json \
    -e PUID=$(id -u) \
    -e PGID=$(id -g) \
    -p 8080:80 \
    --name=share \
    --privileged=true \
    --restart always \
filebrowser/filebrowser:v2-s6
```

容器内文件夹**/srv**映射的**/yalida**目录就是站点根目录，需要分享的文件放在**/yalida**目录下即可。

映射的8080端口不要和其他服务冲突，同时要在在宝塔和云平台放行端口。

最后，可以通过ip+端口来访问filebrowser了，初始用户和密码都是admin。

<br/>

## 配置FileBrowser

去Setting里面修改语言为中文，点击update，然后修改密码，点击更新

<br/>

可以开启用户注册、设定用户权限、自定义品牌信息，可以建立多个用户访问，同时可以指定权限和目录范围。这里的[**.**]代表就是根目录。

![](https://blogs-1302550430.cos.ap-guangzhou.myqcloud.com/images/202204110838617.png/webp)

<br/>

在 设置-全局设置-品牌-实例名称 进行修改

![](https://blogs-1302550430.cos.ap-guangzhou.myqcloud.com/images/202204110838611.png/webp)

<br/>

在映射的根目录yalida下新建一个style文件夹，来管理自定义品牌信息，logo.svg和img目录，custom.css用来自定义样式，目录树如下：

```
├── yalida
│   └── style
│       ├── custom.css
│       └── img
│           ├── icons
│           └── logo.svg
```

<br/>

由于是Docker部署，所以品牌信息文件夹路径填/srv/style，同时勾选禁用外部链接选项

![](https://blogs-1302550430.cos.ap-guangzhou.myqcloud.com/images/202204110838612.png/webp)

<br/>

logo.svg主要是控制站点的登录logo和管理面板左上角的logo，如果想修改favicon图标，可以在/style/img/icons目录下定义不同的icon图标，可以参考[官方文档](https://github.com/filebrowser/frontend/tree/master/public/img/icons)，推荐一个[网站图标生成器](https://realfavicongenerator.net/)，可以很容易生成这些文件。

![](https://blogs-1302550430.cos.ap-guangzhou.myqcloud.com/images/202204111027677.png)

