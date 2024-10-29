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