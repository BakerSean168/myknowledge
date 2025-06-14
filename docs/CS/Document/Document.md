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

## other

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
| `docker stop $(docker ps -aq)` | 停止所有的容器 |
| `docker rm $(docker ps -aq)` | 删除所有的容器 |
| `docker container prune -f` | 删除所有停止的容器 |
| `docker image prune -f -a` | 删除所有不使用的镜像 |
| `docker rmi $(docker images -q)` | 删除所有的镜像 |

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

# virtualenv

*windows下的python包管理器*

## virtualenv 常用命令

| 命令 | 作用 |
| --- | --- |
| `pip install virtualenv` | 安装 `virtualenv` |
| `virtualenv myenv` | 创建一个名为 `myenv` 的虚拟环境 |
| `virtualenv -p /usr/bin/python3.8 myenv` | 指定 python 环境为 3.8 |
| `source myenv/bin/activate` | 激活虚拟环境（Unix 或 MacOS） |
| `myenv\Scripts\activate` | 激活虚拟环境（Windows） |
| `pip install package_name` | 在虚拟环境中安装包 |
| `pip list` | 列出虚拟环境中已安装的包 |
| `deactivate` | 退出虚拟环境 |
| `rm -rf myenv` | 删除虚拟环境 |

[详细命令查看文档](https://virtualenv.pypa.io/en/latest/cli_interface.html#cli-flags)

# 传输文件

有ssh服务时，可以直接用scp命令传输文件:

```powershell
scp -i ~/.ssh/code.pem -r root@47.108.204.117:/output1 D:/
scp -i ~/.ssh/XiangGangVPS2v1g.pem -r ./dist root@8.218.51.159:/
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

# dirsearch

| 命令 | 说明 |
| --- | --- |
| `dirsearch -u <URL>` | 对指定 URL 进行目录和文件暴力破解 |
| `dirsearch -e <EXTENSIONS>` | 指定要搜索的文件扩展名（例如：php, html, js） |
| `dirsearch -w <WORDLIST>` | 指定要使用的字典文件 |
| `dirsearch -t <THREADS>` | 指定线程数以加快扫描速度 |
| `dirsearch -r` | 递归扫描子目录 |
| `dirsearch -x <CODES>` | 排除指定的 HTTP 状态码 |
| `dirsearch -i <CODES>` | 仅包含指定的 HTTP 状态码 |
| `dirsearch -f` | 强制显示找到的所有路径，即使是状态码 403/401 |
| `dirsearch -o <OUTPUT_FILE>` | 将扫描结果输出到指定文件 |
| `dirsearch --proxy <PROXY>` | 使用指定的代理服务器进行扫描 |
| `dirsearch --timeout <TIMEOUT>` | 设置请求超时时间 |
| `dirsearch --user-agent <USER_AGENT>` | 设置自定义的 User-Agent |

python 版本的为 `python dirsearch.py ...`

# 域名基础知识

## 域名结构

一个完整的域名由多个部分组成，这些部分由点号（.）分隔。域名的结构通常包括以下几个部分：

1. **顶级域名（TLD）**：这是域名的最后一部分，例如 `.com`、`.org`、`.net` 等。顶级域名分为两类：通用顶级域名（gTLD）和国家代码顶级域名（ccTLD）。
2. **二级域名**：这是顶级域名前面的部分，例如 `example.com` 中的 `example`。二级域名通常由域名注册人选择。
3. **子域名**：这是二级域名前面的部分，用于进一步划分域名空间。例如 `blog.example.com` 中的 `blog` 是 `example.com` 的子域名。

## 域名注册

域名需要通过域名注册机构进行注册。注册机构负责管理和维护域名的注册信息。常见的域名注册机构包括 GoDaddy、Namecheap、Google Domains 等。

## DNS（域名系统）

域名系统（DNS）是将域名转换为 IP 地址的系统。当用户在浏览器中输入域名时，DNS 会将该域名解析为对应的 IP 地址，从而找到相应的服务器并加载网站内容。

## 域名解析过程

1. 用户在浏览器中输入域名。
2. 浏览器向本地 DNS 服务器发送查询请求。
3. 本地 DNS 服务器检查缓存中是否有该域名的解析记录。
4. 如果缓存中没有记录，本地 DNS 服务器向根 DNS 服务器发送查询请求。
5. 根 DNS 服务器返回顶级域名服务器的地址。
6. 本地 DNS 服务器向顶级域名服务器发送查询请求。
7. 顶级域名服务器返回权威 DNS 服务器的地址。
8. 本地 DNS 服务器向权威 DNS 服务器发送查询请求。
9. 权威 DNS 服务器返回域名对应的 IP 地址。
10. 本地 DNS 服务器将 IP 地址返回给浏览器。
11. 浏览器使用 IP 地址向服务器发送请求并加载网站内容。

## 常见的域名记录类型

1. **A 记录**：将域名映射到 IPv4 地址。
2. **AAAA 记录**：将域名映射到 IPv6 地址。
3. **CNAME 记录**：将一个域名别名映射到另一个域名。
4. **MX 记录**：指定邮件服务器的地址。
5. **TXT 记录**：存储任意文本数据，常用于域名验证和安全设置。

了解这些基础知识可以帮助你更好地理解和管理域名。

# Monaco Editor 的使用

## executeEdits（） 方法

```ts
import { ref } from 'vue'
import MonacoEditor from 'monaco-editor-vue3'
import * as monaco from 'monaco-editor' // 必须引入 monaco 核心

const value = ref('Test')
const editor = ref<monaco.editor.IStandaloneCodeEditor>() // 严格类型

const editorDidMount = (instance: monaco.editor.IStandaloneCodeEditor) => {
  editor.value = instance
  const editorElement = instance.getDomNode()
  
  editorElement.addEventListener('paste', (e: ClipboardEvent) => {
    e.preventDefault() // 关键：阻止默认粘贴
    
    const clipboardData = e.clipboardData
    if (!clipboardData) return
    
    // 获取当前光标位置
    const position = instance.getPosition()
    if (!position) return
    
    // 创建正确的 Range 对象
    const range = new monaco.Range(
      position.lineNumber,
      position.column,
      position.lineNumber,
      position.column
    )
    
    // 执行编辑操作
    instance.executeEdits('paste-operation', [{
      range: range,
      text: '插入的内容',
      forceMoveMarkers: true // 保持后续标记位置
    }])
    
    // 更新光标位置
    const newPosition = position.delta(0, '插入的内容'.length)
    instance.setPosition(newPosition)
  })
}
```
1. 使用 monaco 核心创建 Range
2. 使用 editor 实例来调用 executeEdits 方法

### executeEdits 参数详解

方法签名  
```ts
executeEdits(
  source: string, //操作来源标识 
  edits: IIdentifiedSingleEditOperation[], // 操作集合 
  endCursorState?: Selection[] | null // 编辑后光标位置状态
): void
```

### 编辑操作对象详解

```ts
interface IIdentifiedSingleEditOperation {
  range: IRange;                   // 编辑范围
  text: string;                    // 插入文本
  forceMoveMarkers?: boolean;      // 是否移动标记
  identifier?: ITextModelResolvedOptions;
}

// 创建范围需要 4 个参数：
// startLineNumber, startColumn, endLineNumber, endColumn
const range = new monaco.Range(
  当前行号, 
  当前列号, 
  当前行号, 
  当前列号
)

forceMoveMarkers: true 
// 表示插入文本后，后面的标记（如断点）会跟随移动
// 如果设为 false，插入文本后的标记保持原位置
```