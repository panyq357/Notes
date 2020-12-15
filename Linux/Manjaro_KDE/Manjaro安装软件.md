# 安装软件

## 安装Vim

Manjaro-KDE没有自带Vim，用pacman安装即可。

````bash
sudo pacman -S vim
````

装完后直接运行会提示找不到一个文件：``libperl.so``。

应该是由于Vim需要用到Perl的一些东西，而Manjaro-KDE也没自带Perl，所以还得装Perl。

````bash
sudo pacman -S perl
````

然后Vim就可以运行了。

## 安装IBus和sunpinyin

用pacman安装即可。

````bash
sudo pacman -S ibus ibus-sunpinyin
````

安装完成后，还要往``~/.bashrc``里添加有关输入法的变量。

````bash
export GTK_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
export QT_IM_MODULE=ibus
````

这样就安装完成了，接下来设置开机自启动。

在``设置-开机和关机-自动登陆``处点``添加脚本``按钮，然后输入IBus的守护进程的绝对地址即可。

````bash
/usr/bin/ibus-daemon
````

确定后，IBus即可开机自起了。
