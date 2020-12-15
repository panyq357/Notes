# 配置PyPI源

## 升级pip

先查看pip的版本：``python3 -m pip -V``

如果版本低于10，便需要升级。

临时使用阿里云镜像站升级pip：``python3 -m pip install -i https://mirrors.aliyun.com/pypi/simple/ -U pip``

## 配置源

命令：``python3 -m pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/``

或者也可以直接把以下内容直接添加到``~/.pip/pip.conf``里。

````text
[global]
index-url=https://mirrors.aliyun.com/pypi/simple/

[install]
trusted-host=mirrors.aliyun.com
````

（后两行是aliyun的教程里写的，用处不明，只添加前两行即可）
