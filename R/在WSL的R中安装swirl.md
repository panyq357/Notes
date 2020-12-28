# 在 WSL 的 R 中安装 swirl

[swirl](https://swirlstats.com/) 是一个优秀的用于学习 R 语言的包，它提供了一个互动式的学习环境，用户只需跟着提示输入代码，便能快速掌握基本的 R 语言知识。

这里记录了在 WSL1-Ubuntu20.04 中安装 swirl 的过程。（这里默认 R 已经安装好了。）

首先，打开 R 解释器或 RStudio，在 R 的终端中安装 swirl。

````R
> install.pakage("swirl") # 安装一个叫 "swirl" 的包。
````

之后会开始安装一大堆包，但是有一些包会安装失败。这是由于 WSL 缺少一些 swirl 依赖的软件。

````R
Warning messages:
1: In install.packages("swirl") :
  installation of package ‘curl’ had non-zero exit status
2: In install.packages("swirl") :
  installation of package ‘openssl’ had non-zero exit status
3: In install.packages("swirl") :
  installation of package ‘RCurl’ had non-zero exit status
4: In install.packages("swirl") :
  installation of package ‘httr’ had non-zero exit status
5: In install.packages("swirl") :
  installation of package ‘swirl’ had non-zero exit status
````

经过摸索，确定需要再安装以下软件。

````bash
sudo apt install libcurl4-openssl-dev
sudo apt install libssl-dev
````

安装完后，按开头的方法重新安装一遍 swirl。

这回应该就能成功安装了，接下来，在 R 语言解释其中执行以下命令就能启动 swirl 学习环境了。

````R
> library("swirl")
> swirl()
````

参考：

1. <https://stackoverflow.com/questions/42115972/configuration-failed-because-libcurl-was-not-found>
2. <https://github.com/rocker-org/rocker/issues/124>
