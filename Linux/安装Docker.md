# 安装Docker

## 一、安装Docker CE本体

````bash
# step 1: 安装必要的一些系统工具
sudo apt update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
# step 2: 安装GPG证书
curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
# Step 3: 写入软件源信息（此处的软件源只是Docker CE的软件源，不是Docker Hub的镜像）
sudo add-apt-repository "deb [arch=amd64] https://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
# Step 4: 更新并安装Docker-CE
sudo apt-get -y update
sudo apt-get -y install docker-ce
````

至此Docker CE就安装好了。

## 二、使用阿里云的容器镜像服务

首先，在控制台中找到“容器镜像服务”，进入并设置Registry密码。  
然后，在终端中登录。  

````bash
sudo docker login --username=阿里云用户名 registry.cn-beijing.aliyuncs.com
````

最后，修改``/etc/docker/daemon.json``来使用加速器。

````bash
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["加速器地址"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
````

至此，加速器就配置好了。

## 其他

### 1. 安装docker-compose

````bash
curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-`uname -s`-`uname -m`" > /usr/local/bin/docker-compose
````

(阿里云从github下载东西会很慢)

## 来自

1. <https://edu.aliyun.com/course/426>
2. <https://docs.docker.com/engine/install/ubuntu/>
3. <https://developer.aliyun.com/mirror/docker-ce>
4. <https://cr.console.aliyun.com/cn-beijing/instances/mirrors>
