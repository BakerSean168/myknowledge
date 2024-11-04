# 浏览器搜索技巧

| 技巧 | 说明 |
| --- | --- |
| 去广告搜索 | 使用 `intitle:(关键词)` |
| 限定文件类型 | 使用 `(关键词) filetype:(文件类型)` |
|  | 常见文件类型: |
|  | - `pdf`: PDF文件 |
|  | - `xls`: Excel文件 |
|  | - `ppt`: PowerPoint文件 |
|  | - `doc`: Word文件 |
|  | - `txt`: 文本文档 |
| 关键词包含在正文中 | 使用 `intext:(关键词)` |
| 限定搜索网站 | 使用 `(关键词) inurl:(网站类型)` |
|  | 常见网站类型: |
|  | - `.com`: 商业组织和公司 |
|  | - `.net`: 网络服务商 |
|  | - `.gov`: 政府部门 |
|  | - `.org`: 非营利性组织 |
|  | - `.int`: 国际组织 |
|  | - `.edu`: 教育部门 |
| 限定搜索时间 | 如需搜索2018-2019年，使用 `2018..2019` |
|  | 即 `(开始时间)..(结束时间)` |

注：以上搜索方式可复合使用
注：以上搜索方式可复合使用

# cmd常用命令

| 命令 | 说明 |
| --- | --- |
| `dxdiag` | 查看电脑系统属性 |
| `systeminfo` | 查看系统信息 |
| `wmic bios` | 查询 BIOS 详细信息 |
| `wmic cpu` | 查看 CPU 详细信息 |
| `wmic cpu list brief` | 查看 CPU 型号 |
| `wmic memorychip` | 查看内存详细信息 |
| `wmic memorychip list brief` | 查看内存条数 |
| `wmic memcache list brief` | 查看缓存内存 |
| `wmic diskdrive` | 查看磁盘详细信息 |
| `wmic logicaldisk` | 查看盘符格式大小以及剩余空间 |
| `shutdown /s` | 关机 |
| `shutdown /r` | 重启 |
| `shutdown /l` | 注销 |
| `shutdown /h /f` | 休眠 |
| `shutdown /a` | 取消关机 |
| `shutdown /s /t 3600` | 定时关机（3600 秒后关机） |

# VSCode 快捷键

| 快捷键 | 说明 |
| --- | --- |
| `Alt + 鼠标点击` | 在每一个点击的地方添加输入光标 |
| `Alt + Shift + 鼠标左键按住拖动` | 竖列多行选择。先选择起始点，然后按住 Alt + Shift 加上左键按住拖动。 |
| `鼠标中键选中多行` | 效果和 Alt + Shift + 鼠标左键按住拖动 一样，不过不用先选择起始点，而是鼠标浮动到哪，按住鼠标中键，起始点就是哪里。 |
| `Ctrl + D` | 逐一查找并选中，您选中的内容。 |
| `Ctrl + U` | 回退到上一个 Ctrl + D 选中的内容 |
| `Ctrl + Shift + L` | 类似 Ctrl + D, 不过这是立即选中全部匹配项 |
| `Shift + Alt + i` | 为选中的多行代码末尾插入光标 |

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

# docker
[docker镜像查找](https://hub.docker.com/)

| 命令 | 说明 |
| --- | --- |
| `docker pull [image]` | 从 Docker 仓库中拉取镜像 |
| `docker images` | 列出本地的所有镜像 |
| `docker run [options] [image]` | 运行一个容器 |
| `docker stop [container]` | 停止一个运行中的容器 |
| `docker restart [container]` | 重启一个容器 |
| `docker ps` | 列出当前运行的容器 |
| `docker rm [container]` | 删除一个停止的容器 |
| `docker rmi [image]` | 删除一个镜像 |
| `docker exec -it [container] /bin/bash` | 进入一个运行中的容器 |
| `docker-compose up -d` | 启动 Docker Compose 服务 |
| `docker-compose down` | 停止 Docker Compose 服务 |


## create mysql container
```
docker run -p 3306:3306 --name mysql --privileged=true \
  	-v /mydata/mysql/log:/var/log/mysql \
  	-v /mydata/mysql/data:/var/lib/mysql \
  	-v /mydata/mysql/conf:/etc/mysql/conf.d \
  	-e MYSQL_ROOT_PASSWORD=root \
  	-d mysql
```
查看mysql日志：docker logs -f mysql

## create redis
```
mkdir -p /mydata/redis/conf
touch /mydata/redis/conf/redis.conf
  
docker run -p 6379:6379 --name redis -v /mydata/redis/data:/data \
-v /mydata/redis/conf/redis.conf:/etc/redis/redis.conf \
-d redis redis-server /etc/redis/redis.conf
  	
docker exec -it redis redis-cli //redis镜像执行redis-cli命令连接
```

# hadoop



# nvm
*windows下的node.js版本管理器*

| 命令 | 说明 |
| --- | --- |
| `nvm list` | 查看已经安装的版本 |
| `nvm list installed` | 查看已经安装的版本 |
| `nvm list available` | 查看网络可以安装的版本 |
| `nvm arch` | 查看当前系统的位数和当前nodejs的位数 |
| `nvm install [arch]` | 安装制定版本的node 并且可以指定平台 version 版本号 arch 平台 |
| `nvm on` | 打开nodejs版本控制 |
| `nvm off` | 关闭nodejs版本控制 |
| `nvm proxy [url]` | 查看和设置代理 |
| `nvm node_mirror [url]` | 设置或者查看setting.txt中的node_mirror，如果不设置的默认是 https://nodejs.org/dist/ |
| `nvm npm_mirror [url]` | 设置或者查看setting.txt中的npm_mirror,如果不设置的话默认的是：https://github.com/npm/npm/archive/. |
| `nvm uninstall` | 卸载指定的版本 |
| `nvm use [version] [arch]` | 切换指定的node版本和位数 |
| `nvm root [path]` | 设置和查看root路径 |
| `nvm version` | 查看当前的版本 |.

# virtualenv
*windows下的python包管理器*

create
virtualenv --python route env_name
run
.\env_name\Scripts\activate
stop
deactivate


# 传输文件
```
有ssh服务时，可以直接用scp命令传输文件:

```powershell
scp -i ~/.ssh/code.pem -r root@47.108.204.117:/output1 D:/
```
解释：
- -i ~/.ssh/code.pem：指定私钥文件路径。
- -r：递归复制整个目录（可以传输文件夹）。
- root@47.108.204.117:/output1：云服务器上的目录路径。
- D:/：Windows 本地目录路径。