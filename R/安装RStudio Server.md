# 安装 RStudio Server

这里记录了在 WSL-Ubuntu-20.04 中安装 RStudio Server 的过程。

虽然 RStudio 官网的[教程](https://rstudio.com/products/rstudio/download-server/)已经很简单了，但是图省事的话也可以用下面这两行命令。

````bash
sudo apt install r-base # 安装 R 语言及相关软件。
````

````bash
sudo apt install rstudio-server # 安装 RStudio Server。
````

安装完后这样启动 RStudio Server。

````bash
rstudio-server start
````

然后打开浏览器，访问 <http://localhost:8787/> 即可，初次访问会提示输入用户名和密码，其实就是 Linux 的用户名和密码啦。
