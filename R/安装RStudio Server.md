# 安装 RStudio Server

这里记录了在 WSL-Ubuntu-20.04 中安装 RStudio Server 的过程。

照着 RStudio 官网的[教程](https://support.rstudio.com/hc/en-us/articles/360049776974-Using-RStudio-Server-in-Windows-WSL2)做即可。
<!-- 
````bash
sudo apt install r-base # 安装 R 语言及相关软件。
````

````bash
sudo apt-get install gdebi-core
wget https://download2.rstudio.org/server/bionic/amd64/rstudio-server-1.4.1103-amd64.deb
sudo gdebi rstudio-server-1.4.1103-amd64.deb # 安装 RStudio Server。
````

安装完后这样启动 RStudio Server。

````bash
rstudio-server start
````

然后打开浏览器，访问 <http://localhost:8787/> 即可，初次访问会提示输入用户名和密码，其实就是 Linux 的用户名和密码啦。 -->
