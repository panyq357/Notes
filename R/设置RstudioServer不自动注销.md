# 设置 RStudio Server 不自动注销

按照 RStudio Server 的默认设置，在用户关闭浏览器一段时间后，服务器端就会暂停用户的会话。当用户再次打开 RStudio Server 的页面时就又需要输入账号密码了。

通过修改 RStudio Server 的配置文件 ``/etc/rstudio/rserver.conf``，在其中添加以下语句。

```txt
auth-timeout-minutes=0
auth-stay-signed-in-days=30
```

保存退出后重启 RStudio Server。

```bash
sudo rstudio-server restart
```

再重新通过浏览器登录 RStudio Server 时，勾选框旁边的说明文字就变了。

参考：<https://github.com/rstudio/rstudio/issues/5449#issuecomment-637586731>