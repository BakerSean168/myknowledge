<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Andriod](#andriod)
- [Windows](#windows)
  - [environment](#environment)
    - [python](#python)
      - [管理器](#管理器)
      - [打包器](#打包器)
- [Linux](#linux)
    - [shell](#shell)
      - [usage](#usage)
    - [vim](#vim)
    - [删除编译软件](#删除编译软件)
      - [mysql](#mysql)
        - [start](#start)
        - [Mysql user management](#mysql-user-management)
      - [nginx](#nginx)
        - [Web服务器](#web服务器)
          - [location](#location)
          - [反向代理](#反向代理)
          - [负载均衡](#负载均衡)
      - [docker](#docker)
        - [vulhub靶场](#vulhub靶场)
        - [create mysql container](#create-mysql-container)
        - [create redis](#create-redis)
      - [mybatis](#mybatis)
  - [Centos](#centos)
    - [包管理器](#包管理器)
- [Ubuntu](#ubuntu)
    - [包管理器](#包管理器-1)

<!-- /code_chunk_output -->



[How to install software in linux](https://linuxize.com/)

# Andriod
shizuku
scene



# Windows


## environment

### node.js
#### 管理器
**nvm**
常用命令
nvm list	查看已经安装的版本
nvm list installed	查看已经安装的版本
nvm list available	查看网络可以安装的版本
nvm arch	查看当前系统的位数和当前nodejs的位数
nvm install [arch]	安装制定版本的node 并且可以指定平台 version 版本号 arch 平台
nvm on	打开nodejs版本控制
nvm off	关闭nodejs版本控制
nvm proxy [url]	查看和设置代理
nvm node_mirror [url]	设置或者查看setting.txt中的node_mirror，如果不设置的默认是 https://nodejs.org/dist/
nvm npm_mirror [url]	设置或者查看setting.txt中的npm_mirror,如果不设置的话默认的是：https://github.com/npm/npm/archive/.
nvm uninstall	卸载指定的版本
nvm use [version] [arch]	切换指定的node版本和位数
nvm root [path]	设置和查看root路径
nvm version	查看当前的版本


### python
#### 管理器
**virtualenv**
create
virtualenv --python route env_name
run
.\env_name\Scripts\activate
stop
deactivate

#### 打包器

py2exe
Nuitka
pyinstall

# Linux



### shell
cat /etc/shells  查看系统内的shell
可以使用路径切换到相应的shell版本
echo $SHELL      查看当前系统变量中显示的shell版本   
echo $0          当前正在执行的脚本名称

#### usage
vi hello.sh //create a sh script file
chmod a+x hello.sh
./hello.sh

### vim
- 显示行号 :set number!
- 删除当前行 dd
- 清空文件内容
    - gg		# 跳至文件首行
    - dG		# 删除光标所在行到末尾行内容，d删除，G跳转到文件末尾行

### 删除编译软件
1. make uninstall 执行作者编写的卸载文件
2. build目录下，执行：```xargs rm < install_manifest.txt```
make install之后，build目录下会有一个install_mainfest.txt的文件, 记录了安装的所有内容及路径，
执行 xargs rm < install_manifest.txt 就可以了。
如果没有这个文件，可以自己重新make install，从log中过滤出install的安装路径信息，保存到unistall.txt中，再执行xargs rm < unistall.txt即可。


#### mysql

##### start
1. use apt update the package
2. use `apt-cache serach mysql-server` to fing the package
3. use `sudo apt install mysql-server-8.0` install mysql
    **setting the root password：**
    ```
    sudo mysql;
    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'My7Pass@Word_9_8A_zE';
    ```
    **MySQL 8.xx 的关键配置文件和端口:**
    - mysql.service，这是服务的名称。您可以使用以下 systemctl 命令来管理它
    sudo systemctl start mysql.service
    sudo systemctl stop mysql.service
    sudo systemctl restart mysql.service
    sudo systemctl status mysql.service
    - /etc/mysql/ - MySQL 服务器的主要配置目录。
    - /etc/mysql/my.cnf - MySQL 数据库服务器的配置文件。编辑 .my.cnf ($HOME/.my.cnf) 文件来设置用户特定的选项。以下两个目录中的设置可以覆盖它： /etc/mysql/conf.d//etc/mysql/mysql.conf.d/
    - TCP/3306 端口 - TCP/3306 是 MySQL 服务器的默认网络端口，出于安全考虑，它绑定在 127.0.0.1 上，可以更改这个设置，之后就可以通过在 /run/mysqld/ 目录下设置的 localhost 套接字来访问 MySQL 服务器。
4. enhacing the security of mysql
`sudo mysql_secure_installation`
5. controlling the status of mysql
```
systemctl enable mysql.service
systemctl start mysql.service
systemctl status mysql.service
systemctl stop mysql.service
systemctl restart mysql.service
```
6. Configuring the MySQL 8 Server
Edit the /etc/mysql/mysql.conf.d/mysqld.cnf file with a text editor
` vim /etc/mysql/mysql.conf.d/mysqld.cnf`
##### Mysql user management
- add user
`create user username identified by 'password';`
create user zhangsan identified by 'zhangsan';
- grant (`show grants;//查询用法`)
`grant privilegesCode on dbName.tableName to username@host;`
grant all privileges on zhangsanDb.* to zhangsan@'%';
flush privileges;
`show grants for user;`
show grants for 'zhangsan';
privilegesCode表示授予的权限类型，常用的有以下几种类型：
all privileges：所有权限。
select：读取权限。
delete：删除权限。
update：更新权限。
create：创建权限。
drop：删除数据库、数据表权限。
dbName.tableName表示授予权限的具体库或表，常用的有以下几种选项：
.：授予该数据库服务器所有数据库的权限。
dbName.*：授予dbName数据库所有表的权限。
dbName.dbTable：授予数据库dbName中dbTable表的权限。
username@host表示授予的用户以及允许该用户登录的IP地址。其中Host有以下几种类型：
localhost：只允许该用户在本地登录，不能远程登录。
%：允许在除本机之外的任何一台机器远程登录。
192.168.52.32：具体的IP表示只允许该用户从特定IP登录。
password指定该用户登录时的面。
flush privileges表示刷新权限变更。
- change passwoed
`update mysql.user set password = password('zhangsannew') where user = 'zhangsan' and host = '%';`
- delete user
`drop user zhangsan@'%';`
- 常用命令组
`create user zhangsan identified by 'zhangsan';`
`grant all privileges on zhangsanDb.* to zhangsan@'%' identified by 'zhangsan';`
`flush  privileges;`
创建了用户zhangsan，并将数据库zhangsanDB的所有权限授予zhangsan。如果要使zhangsan可以从本机登录，那么可以多赋予localhost权限：
`grant all privileges on zhangsanDb.* to zhangsan@'localhost' identified by 'zhangsan';`
#### nginx
/etc/nginx

nginx -t 检测文件配置是否有问题
nginx -s reload 重新加载

##### Web服务器

nginx.conf
```
events{}

http{
    
        include /etc/nginx/mine.types;
        include /etc/nginx/conf.d/*.conf;
}
```
/etc/nginx/conf.d/default.conf
```
server {
    listen 80;
    server_name localhost;

    location /app {
        root /var/www/localhost;
    }
}
```
###### location


**路径匹配**

存在：
localhost/app/index.html
localhost/apple/index.html
1. 
location /app {
    root /var/www/localhost;
}  //匹配路径包含 /app 的地址

URL localhost/app //在app当前所在的文件夹下寻找，  不能找到
URL localhost/app/ //在app文件夹中寻找，  能找到
URL localhost/app/index.html  //能访问
URL localhost/apple/index.html  //能访问
//更灵活但容易暴露其他文件
2. 
location = /app/index.html {
    root /var/www/localhost;
}  //访问的路径要与实际文件完全一致
//不太灵活
3. 
location ~ /app/index[2-4].html {
    root /var/www/localhost;
}  //使用正则表达式

*匹配优先级*：
1. = 精确
2. ^~ 优先前缀
3. ~和~* 正则
4. 空格 普通前缀

**重定向**

1. return
location / {
    return 307 /app/index.html
}

2. rewrite
rewrite /temp /app/index.html

3. try_files
location / {
    try_files $url $url/ =404;
} //先匹配第一个，失败后第二个，最后404；可通过 error_page 404 route 自定义404页面

###### 反向代理

```
server {
    listen 80;
    server_name localhost;

    root /var/www/localhost;
    index index.html;
    error_page 404 /404.html;

    location app1 {
        proxy_pass http://localhost:3000;
    }

    location app2 {
        proxy_pass http://localhost:3001;
    }
}
```

###### 负载均衡

```
upstream backend-servers {
    server localhost:3000 weight=2;
    server localhost:3001 weight=6;
}

server {
    listen 80;
    server_name localhost;

    root /var/www/localhost;
    index index.html;
    error_page 404 /404.html;

    location / {
        proxy_pass http://backend-servers;
    }

}
```

#### docker


##### vulhub靶场
启动环境
root@ubuntu:/# cd /
root@ubuntu:/# cd vulhub/
root@ubuntu:/vulhub# cd httpd/
root@ubuntu:/vulhub/httpd# cd CVE-2017-15715/
root@ubuntu:/vulhub/httpd/CVE-2017-15715# docker-compose up -d
root@ubuntu:/vulhub/httpd/CVE-2017-15715# docker-compose up -d
结束环境
root@ubuntu:/vulhub/httpd/CVE-2017-15715# docker-compose down
原文链接：https://blog.csdn.net/m0_48907714/article/details/123745656

##### create mysql container
```
docker run -p 3306:3306 --name mysql --privileged=true \
  	-v /mydata/mysql/log:/var/log/mysql \
  	-v /mydata/mysql/data:/var/lib/mysql \
  	-v /mydata/mysql/conf:/etc/mysql/conf.d \
  	-e MYSQL_ROOT_PASSWORD=root \
  	-d mysql
```
查看mysql日志：docker logs -f mysql

##### create redis
```
mkdir -p /mydata/redis/conf
touch /mydata/redis/conf/redis.conf
  
docker run -p 6379:6379 --name redis -v /mydata/redis/data:/data \
-v /mydata/redis/conf/redis.conf:/etc/redis/redis.conf \
-d redis redis-server /etc/redis/redis.conf
  	
docker exec -it redis redis-cli //redis镜像执行redis-cli命令连接
```

#### mybatis



## Centos

### 包管理器
- rpm
    ```
    RPM包默认安装路径
    /etc/配置文件安装目录
    /usr/bin/可执行的命令安装目录
    /usr/lib/程序所使用的函数库保存位置
    /usr/share/doc/基本的软件使用手册保存位置
    /usr/share/man/帮助文件保存位置
    ```
- yum

# Ubuntu

### 包管理器
- apt
    ```
    sudo apt update
    sudo apt list --upgradable
    sudo apt upgrade
    ```