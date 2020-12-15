# 配置vsftpd

本文的主要内容为配置服务器的FTP服务，使得用户能够通过FTP从服务器上传下载文件。

vsftpd意为“Very Secure FTP Daemon”，是一个用于服务器端的轻量的FTP服务器软件。本文安装的版本为3.0.3。  

安装vsftpd很简单，只需一条命令。

````bash
sudo apt install vsftpd
````

安装vsftpd后还需要进行一些配置。在配置之前，有一些概念需要说明。

1. chroot：这是一个修改根目录的命令。我们可以通过配置，让vsftpd使用这个命令，限制用户的可访问的空间，以保护系统。
2. FTP的被动模式：当用户通过FTP访问服务器时，服务器会随机地开端口，用户通过访问指定端口就能下载上传文件。WinSCP默认的就是这个模式。我们可以通过设置，限定服务器开放的端口范围。

接下来修改配置文件，vsftpd的配置文件位于``/etc/vsftpd.conf``，我们需要取消一些行的注释，以及添加几行新的设置。  
最终的``/etc/vsftpd.conf``文件的内容（去掉了自带的注释）如下。

````bash
listen=NO
listen_ipv6=YES
anonymous_enable=NO
local_enable=YES
dirmessage_enable=YES
use_localtime=YES
xferlog_enable=YES
connect_from_port_20=YES

# 让用户可以上传文件。
write_enable=YES

# 当用户登陆时，让vsftpd修改用户能看到的根目录，以保护系统的其他部分。
chroot_local_user=YES

secure_chroot_dir=/var/run/vsftpd/empty
pam_service_name=vsftpd
rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
ssl_enable=NO

# 使文件系统为编码格式为UTF-8。
utf8_filesystem=YES

# 限制被动模式下，服务器开放的端口的编号的下限。
pasv_min_port=30000

# 限制被动模式下，服务器开放的端口的编号的上限。
pasv_max_port=31000

# 把用户可见的根目录设置到用户主目录下，这样用户就看不到系统的其他部分了。
user_sub_token=$USER
local_root=/home/$USER

# 让用户可以上传文件到自己的ftp目录下。
allow_writeable_chroot=YES
# 如果没有上面这行，而又启用了chroot，用户就不能上传文件了。
# 而且vsftpd还会检测系统的权限设置，如果用户在服务器的文件系统中在自己的主目录下有写权限就会报错。
````

这样vsftpd就设置好了。

但是vsftpd默认并不让root用户访问，我们需要在Linux下创建新的用户，然后用这个用户访问服务器。

````bash
# 以下命令在需切换到root用户执行。
useradd ftpuser # 创建用户。
passwd ftpuser # 设置用户密码。
mkdir /home/ftpuser # 给用户创建个主目录。
chown ftpuser:ftpuser /home/ftpuser # 把用户家目录的归属交给用户。
````

这样用户就创建完了。

最后开启阿里云安全组中入方向的以下端口。

- 20：数据端口，主动模式下服务器用这个端口传数据给客户端。由于我们通常用被动模式连接服务器，这个端口也可不开。
- 21：控制端口，控制连接的建立，用户的验证等。
- 30000~31000：跟配置文件里写的要一致。被动模式下，服务器通过在这里随机地挑一个端口，让用户连接，来传输数据。

参考：

1. <https://linuxize.com/post/how-to-setup-ftp-server-with-vsftpd-on-ubuntu-18-04/>
2. <https://linux.vbird.org/linux_server/centos6/0410vsftpd.php>
3. <https://blog.csdn.net/bluishglc/article/details/42399439>
