# Gnome 登陆后有两个鼠标指针

此现象已被确认为 BUG 并长期未得到修复。

解决方法来自这个[评论](https://bugs.launchpad.net/ubuntu/+source/mutter/+bug/1873052/comments/7)

方法：修改 ``/etc/gdm3/custom.conf`` 文件，找到 ``WaylandEnable=false``，将其取消注释。

参考：<https://bugs.launchpad.net/ubuntu/+source/mutter/+bug/1873052>