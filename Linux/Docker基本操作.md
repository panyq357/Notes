# Docker基本操作

本篇记录了些常见的Docker命令的用法。

## 进入容器

命令：``docker exec -it MYCONTAINER /bin/bash``  
该命令可以进入到容器内并运行其中的bash。  

- ``-i``：使得容器内的bash能够接受我们的输入。
- ``-t``：提供一个伪终端提示符。

## 用Docker安装Nginx

首先，获取Nginx的镜像。

````bash
docker image pull nginx
````

然后，创建一个Docker的Volume，用来存放Nginx的网页文件和配置文件。

````bash
docker volume create mynginxhtml
docker volume create mynginxconfig
````

查看一下volume的绝对位置。

````bash
docker volume inspect mynginxhtml mynginxconfig
````

回显内容如下：

````bash
[
    {
        "CreatedAt": "2020-10-08T15:52:53+08:00",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/mynginxhtml/_data",
        "Name": "mynginxhtml",
        "Options": {},
        "Scope": "local"
    },
    {
        "CreatedAt": "2020-10-08T15:52:53+08:00",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/mynginxconfig/_data",
        "Name": "mynginxconfig",
        "Options": {},
        "Scope": "local"
    }
]
````

其中，``"Mountpoint"``所指的就是volume的绝对位置。

## 安装Nginx

````bash
docker container run -d \
    -p 80:80 \
    -v mynginxhtml:/usr/share/nginx/html/ \
    -v mynginxconfig:/etc/nginx \
    --name mynginx \
    nginx
````

- ``-d``：在后台运行；
- ``-p``：冒号左侧是本机端口，冒号右侧是要映射的容器端口；
- ``-v``或``--volume``：冒号左侧是Docker的Volume的名字，冒号右侧是要映射的容器的位置；
- ``--name``：安装的container的名字；
- 最后跟上要安装的image的名字。
