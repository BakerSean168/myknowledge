# git

[Pro Git book,这是一本关于如何使用 Git 的优秀图书](https://git-scm.com/book/en/v2)

设置全局 Git 用户名和密码
```
git config --global user.name "Your Name"
git config --global user.email "youremail@yourdomain.com"
```
这些值保存在全局配置文件 ~/.gitconfig 中

确认信息
```
git config --list
user.name=Your Name
user.email=youremail@yourdomain.com
```


1. Always try `git pull --rebase` first
2. if you get a merge conflict,you can undo everything with`git rebase --abort`


# hadoop