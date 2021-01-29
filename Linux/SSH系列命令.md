# SSH 系列命令

此处记录了一些与 SSH 有关的命令的用法。

## ``ssh``

示例：

````bash
ssh -p 12345 root@123.45.67.89
````

## ``ssh-keygen``

## ``ssh-copy-id`` （仅限 Linux，Windows 上没这个命令）

示例：

````bash
ssh-copy-id -p 12345 -i .ssh/id_rsa.pub root@123.45.67.89
````

## ``sftp``
