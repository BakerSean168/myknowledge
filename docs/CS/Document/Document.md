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
## 常见命令
[docker镜像查找](https://hub.docker.com/)

| 命令 | 说明 |
| --- | --- |
| `docker pull [image]` | 从 Docker 仓库中拉取镜像 |
| `docker images` | 列出本地的所有镜像 |
| `docker run [options] [image]` | 运行一个容器 |
| `docker stop [container]` | 停止一个运行中的容器 |
| `docker start [container]` | 启动一个容器 |
| `docker restart [container]` | 重启一个容器 |
| `docker ps [-a]` | 列出当前运行（所有）的容器 |
| `docker rm [container]` | 删除一个停止的容器 |
| `docker rmi [image]` | 删除一个镜像 |
| `docker exec -it [container] /bin/bash` | 进入一个运行中的容器 |
| `docker-compose up -d` | 启动 Docker Compose 服务 |
| `docker-compose down` | 停止 Docker Compose 服务 |

## docker 容器自动重启

重启策略如下

| 命令            | 作用                                      |
| --------------- | ----------------------------------------- |
| `no`            | 默认策略，在容器退出时不重启容器          |
| `on-failure`    | 在容器非正常退出时（退出状态非0），才会重启容器 |
| `on-failure:3`  | 在容器非正常退出时重启容器，最多重启3次   |
| `always`        | 在容器退出时总是重启容器                  | 
| `unless-stopped`| 在容器退出时总是重启容器，但是不考虑在Docker守护进程启动时就已经停止了的容器 |

运行一个容器时添加策略  
```docker run -d --restart 策略 容器```

已经运行的容器添加策略  
```docker container update --restart 策略 容器```

查看容器的重启策略
```docker inspect -f "{{ .HostConfig.RestartPolicy.Name }}" 容器```

查看容器启动次数命令  
```docker inspect -f "{{ .RestartCount }}" 容器```

查看容器最后一次启动时间  
```docker inspect -f "{{ .State.StartedAt }}" 容器```

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

## virtualenv 常用命令

| 命令 | 作用 |
| --- | --- |
| `pip install virtualenv` | 安装 `virtualenv` |
| `virtualenv myenv` | 创建一个名为 `myenv` 的虚拟环境 |
| `source myenv/bin/activate` | 激活虚拟环境（Unix 或 MacOS） |
| `myenv\Scripts\activate` | 激活虚拟环境（Windows） |
| `pip install package_name` | 在虚拟环境中安装包 |
| `pip list` | 列出虚拟环境中已安装的包 |
| `deactivate` | 退出虚拟环境 |
| `rm -rf myenv` | 删除虚拟环境 |


# 传输文件

有ssh服务时，可以直接用scp命令传输文件:

```powershell
scp -i ~/.ssh/code.pem -r root@47.108.204.117:/output1 D:/
```

解释：
- -i ~/.ssh/code.pem：指定私钥文件路径。
- -r：递归复制整个目录（可以传输文件夹）。
- root@47.108.204.117:/output1：云服务器上的目录路径。
- D:/：Windows 本地目录路径。

# hadoop

## hadoop 文件系统

HDFS Shell CLI 支持多种文件系统，包括本地文件系统（file：///）、分布式文件系统（hdfs：//nn：8020）等  
没有指定前缀，默认读取环境变量中 fs.defaultFS 属性的值作为默认文件系统。

## hadoop 常用命令

| 命令 | 作用 |
| --- | --- |
| `hadoop version` | 查看 Hadoop 版本信息 |
| `hadoop fs -ls /path` | 列出 HDFS 中指定路径的文件和目录 |
| `hadoop fs -mkdir /path` | 在 HDFS 中创建目录 |
| `hadoop fs -put localfile /path` | 将本地文件上传到 HDFS |
| `hadoop fs -get /path localfile` | 从 HDFS 下载文件到本地 |
| `hadoop fs -rm /path` | 删除 HDFS 中的文件或目录 |
| `hadoop fs -rmdir /path` | 删除 HDFS 中的空目录 |
| `hadoop fs -cat /path` | 显示 HDFS 中文件的内容 |
| `hadoop fs -copyFromLocal localfile /path` | 将本地文件复制到 HDFS |
| `hadoop fs -copyToLocal /path localfile` | 将 HDFS 文件复制到本地 |
| `hadoop fs -moveFromLocal localfile /path` | 将本地文件移动到 HDFS |
| `hadoop fs -moveToLocal /path localfile` | 将 HDFS 文件移动到本地 |
| `hadoop fs -chown user:group /path` | 更改 HDFS 文件或目录的所有者和组 |
| `hadoop fs -chmod permissions /path` | 更改 HDFS 文件或目录的权限 |
| `hadoop fs -chgrp group /path` | 更改 HDFS 文件或目录的组 |
| `hadoop fs -du /path` | 显示 HDFS 中目录的磁盘使用情况 |
| `hadoop fs -df /path` | 显示 HDFS 的磁盘空间使用情况 |
| `hadoop fs -stat /path` | 显示 HDFS 文件或目录的状态信息 |
| `hadoop fs -tail /path` | 显示 HDFS 文件的最后部分内容 |
| `hadoop fs -test -e /path` | 测试 HDFS 路径是否存在 |
| `hadoop fs -test -d /path` | 测试 HDFS 路径是否为目录 |
| `hadoop fs -test -f /path` | 测试 HDFS 路径是否为文件 |
| `hadoop fs -text /path` | 将 HDFS 文件内容显示为文本 |
| `hadoop jar myjar.jar [mainClass] args...` | 运行 Hadoop 应用程序 |
| `start-dfs.sh` | 启动 HDFS 服务 |
| `stop-dfs.sh` | 停止 HDFS 服务 |
| `start-yarn.sh` | 启动 YARN 服务 |
| `stop-yarn.sh` | 停止 YARN 服务 |
| `jps` | 查看 Hadoop 相关进程 |


