## 解决用 ``ssh`` 连接服务器后使用某些命令提示 ``manpath`` 错误的问题

用 WSL 2 的 ``ssh`` 连接远程服务器后使用 ``man`` 命令，会出现这样一条语句。

````txt
manpath: can't set the locale; make sure $LC_* and $LANG are correct
````

虽不影响使用，但是很碍眼，解决方法为在 WSL 中执行下面这条命令。

````bash
sudo dpkg-reconfigure locales
````

然后在粉色的界面中中按 ``Tab`` 选中 ``OK``，回车后再选择 ``en_US.UTF-8``，再回车。

退出粉色界面后，终端中会打印这样一段信息。

````bash
Generating locales (this might take a while)...
  en_US.UTF-8... done
Generation complete.
````

然后再用 ``ssh`` 试试，就没有错误了。

参考：<https://blog.csdn.net/everblog/article/details/79765313>