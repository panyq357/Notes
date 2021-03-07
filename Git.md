# Git

## 常用命令

### 设置用户名和 E-mail

````bash
git config --global user.name YOURUSERNAME
git config --global user.email YOUREMAIL
````

### Github SSH 测试

````bash
ssh -T git@github.com
````

### 修改上次 ``push`` 的提交信息。

来自：<https://blog.csdn.net/ecjtuhq/article/details/80358656>

```bash
git commit --amend 
```

然后会弹出文本编辑器界面，修改完后保存退出。

```bash
git push --force-with-lease origin main
```

然后远程仓库中的提交信息就被修改了。