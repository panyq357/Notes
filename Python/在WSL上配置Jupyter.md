# 在 WSL 上配置 Jupyter

## 安装

``python3 -m pip install jupyterlab`` 即可。

## 修改配置

由于 WSL 不是常规的 Linux 发行版，在 bash 中使用 ``jupyter lab`` 等命令直接启动 Jupyter 时会出错。所以要修改些不适合 WSL 的配置选项。

首先在 bash 中键入 ``jupyter notebook --generate-config``，生成配置文件，其位于 ``~/.jupyter/jupyter_notebook_config.py``。

在这个文件中找到 ``c.NotebookApp.use_redirect_file`` 项目，取消注释，并将值从 ``True`` 改为 ``False`` 。

现在在 bash 中使用 ``jupyter lab`` 已经可以启动了，但是会出现启动信息被吞的现象，这可能是调用浏览器时发生的问题。

## 设置要调用的浏览器

修改 ``~/.bashrc`` 文件，添加一行 ``export BROWSER="/mnt/c/Program Files (x86)/Microsoft/Edge/Application/msedge.exe"``，这使得 Jupyter 能直接找到浏览器并启动。（此处为新 edge 的默认路径）

> 注意：新 Edge 与 WSL2 相性较好，能够自动打开 jupyter lab 的页面，用 Chrome 的话则会打开失败。

然后在 bash 中键入``source ~/.bashrc``，更新环境变量。

现在键入 ``jupyter lab`` 即可启动，启动信息也能完整显示了。
