# Windows Terminal设置

## 添加新的终端

在设置文件``settings.json``中的``profiles``下的``list``中添加对应的内容即可（按需修改）。

GUID可在PowerShell中用``[guid]::NewGuid()``生成。

### 添加Git Bash
````json
{
    "guid": "{abcdabcd-e4cc-4718-a270-ccadc3c21223}",
    "hidden": false,
    "name": "Git Bash", 
    "commandline": "C:\\Program Files\\Git\\bin\\bash.exe -il",
    "icon": "C:\\Program Files\\Git\\mingw64\\share\\git\\git-for-windows.ico",
    "startingDirectory": "%USERPROFILE%"
},
````

### 添加ssh

在添加前最好在cmd下用``ssh-keygen``等命令生成公钥，并把公钥添加到服务器的配置文件里。

````json
{
    "guid": "{abcdabcd-e062-4d91-b17e-b97eeebfaba3}",
    "hiden": false,
    "name": "my server",
    "icon": "ms-appx:///ProfileIcons/{550ce7b8-d500-50ad-8a1a-c400c3262db3}.png",
    "commandline": "ssh -p 端口号 用户名@服务器IP或域名"
},
````