# 解决开机时显示的acpi_video0错误

开机时显示类似于这样的信息。

````txt
Failed to start Load/Save Screen Backlight Brightness of backlight:acpi_video0
````

通过在bash中键入命令查询。

````bash
systemctl status systemd-backlight@backlight:acpi_video0.service
````

发现是因为没有这个设备，所以直接屏蔽这个服务即可。

````bash
sudo systemctl mask systemd-backlight@backlight:acpi_video0
````

参考：<https://blog.csdn.net/grsharp/article/details/105735792>
