
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Centos](#centos)
  - [包管理器：](#包管理器)
  - [vim](#vim)
  - [删除编译软件：](#删除编译软件)
    - [nginx](#nginx)
      - [Web服务器](#web服务器)
        - [location](#location)
        - [反向代理](#反向代理)
        - [负载均衡](#负载均衡)

<!-- /code_chunk_output -->


[How to install software in linux](https://linuxize.com/)

## Centos

### 包管理器：
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

### vim
- 显示行号 :set number!
- 删除当前行 dd
- 清空文件内容
    - gg		# 跳至文件首行
    - dG		# 删除光标所在行到末尾行内容，d删除，G跳转到文件末尾行

### 删除编译软件：
1. make uninstall 执行作者编写的卸载文件
2. build目录下，执行：```xargs rm < install_manifest.txt```
make install之后，build目录下会有一个install_mainfest.txt的文件, 记录了安装的所有内容及路径，
执行 xargs rm < install_manifest.txt 就可以了。
如果没有这个文件，可以自己重新make install，从log中过滤出install的安装路径信息，保存到unistall.txt中，再执行xargs rm < unistall.txt即可。

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