# 改 Vim 的 Tab 键 为 4 个空格。

修改 vim 的配置文件。

````bash
vim /etc/vim/vimrc
````

在文件底部添加以下内容。

````vim
" Tab key == 4 spaces and auto-indent after curly braces in Vim
filetype plugin indent on
" show existing tab with 4 spaces width
set tabstop=4
" when indenting with '>', use 4 spaces width
set shiftwidth=4
" On pressing tab, insert 4 spaces
set expandtab
````

来源：<https://stackoverflow.com/questions/234564/tab-key-4-spaces-and-auto-indent-after-curly-braces-in-vim>
