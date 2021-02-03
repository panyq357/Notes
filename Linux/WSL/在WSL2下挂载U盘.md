# 在 WSL2 下挂载 U 盘

参考：<https://docs.microsoft.com/zh-cn/archive/blogs/wsl/file-system-improvements-to-the-windows-subsystem-for-linux#mounting-drvfs>

````bash
sudo mount -t drvfs D: /mnt/d  # 挂载
sudo umount /mnt/d  # 解除挂载
````
