[How to install software in linux](https://linuxize.com/)

# Linus

Debian系列：Debian，Ubuntu  
Redhat系列：RHEL，CentOS，Fedora  
Arch系列  
国产麒麟：飞腾，龙芯，鲲鹏  
Slackware Linux：SUSE  

## shell

`cat /etc/shells`  查看系统内的shell
可以使用路径切换到相应的shell版本
`echo $SHELL`      查看当前系统变量中显示的shell版本   
`echo $0`          当前正在执行的脚本名称
`chsh -s $(which zsh)` 切换为zsh

### Command-Line 日常使用技巧

| 快捷键 | 作用 |
| --- | --- |
| `ctrl-w` | 删除你键入的最后一个单词 |
| `ctrl-u` | 删除行内光标所在位置之前的内容 |
| `alt-b` | 以单词为单位向后移动光标 |
| `alt-f` | 以单词为单位向前移动光标 |
| `ctrl-a` | 将光标移至行首 |
| `ctrl-e` | 将光标移至行尾 |
| `ctrl-k` | 删除光标至行尾的所有内容 |
| `ctrl-l` | 清屏 |
| `man readline` | 查看 Bash 中的默认快捷键 |

- 在 Bash 中，可以通过按 Tab 键实现自动补全参数，使用 ctrl-r 搜索命令行历史记录（按下按键之后，输入关键字便可以搜索，重复按下 ctrl-r 会向后查找匹配项，按下 Enter 键会执行当前匹配的命令，而按下右方向键会将匹配项放入当前行中，不会直接执行，以便做出修改）。
- 为了便于编辑长命令，在设置你的默认编辑器后（例如 export EDITOR=vim），ctrl-x ctrl-e 会打开一个编辑器来编辑当前输入的命令。在 vi 风格下快捷键则是 escape-v。
- pstree -p 以一种优雅的方式展示进程树。

## 包管理器

### Redhat系列

#### rpm

**RPM 包的组成**  

RPM 包通常包含二进制文件、配置文件、文档和其他相关文件。  
RPM 包的文件名通常包含包名、版本号、发布号、架构和扩展名 `.rpm`。  

**RPM 包的命名格式**

格式：`<name>-<version>-<release>.<architecture>.rpm`  
例如：`httpd-2.4.6-90.el7.centos.x86_64.rpm`  

**RPM 包的默认安装路径**

| 目录 | 作用 |
| --- | --- |
| `/etc/` | 配置文件安装目录 |
| `/usr/bin/` | 可执行的命令安装目录 |
| `/usr/lib/` | 程序所使用的函数库保存位置 |
| `/usr/share/doc/` | 基本的软件使用手册保存位置 |
| `/usr/share/man/` | 帮助文件保存位置 |
| `/usr/share/man/` | 帮助文件保存位置 |

##### 常用 RPM 命令

| 命令 | 作用 |
| --- | --- |
| `rpm -ivh package.rpm` | 安装 RPM 包 |
| `rpm -Uvh package.rpm` | 升级 RPM 包 |
| `rpm -e package` | 卸载 RPM 包 |
| `rpm -q package` | 查询已安装的 RPM 包 |
| `rpm -qa` | 列出所有已安装的 RPM 包 |
| `rpm -qi package` | 显示已安装 RPM 包的信息 |
| `rpm -ql package` | 列出已安装 RPM 包的文件 |
| `rpm -qc package` | 列出已安装 RPM 包的配置文件 |
| `rpm -qf /path/to/file` | 查询文件属于哪个 RPM 包 |
| `rpm -V package` | 验证已安装的 RPM 包 |
| `rpm --import /path/to/key` | 导入 GPG 密钥 |
| `rpm -K package.rpm` | 验证 RPM 包的完整性和签名 |

#### yum

**YUM 包管理器**

YUM (Yellowdog Updater, Modified) 是一个基于 RPM 的包管理器，广泛用于 CentOS、RHEL 和 Fedora 等发行版。它的主要特点包括：

- 依赖管理：自动处理包依赖关系，简化软件安装和更新过程。
- 仓库支持：支持多个仓库，可以从不同的源获取软件包。
- 插件系统：支持插件，可以扩展 YUM 的功能。
- 易用性：命令简单易用，适合新手和高级用户。

**YUM 源配置文件**

YUM 源配置文件通常位于 `/etc/yum.repos.d/` 目录下，每个仓库对应一个 `.repo` 文件。每个 `.repo` 文件包含仓库的配置信息。

**YUM 源配置文件示例**

以下是一个典型的 YUM 源配置文件示例：

```ini
[base]
name=CentOS-$releasever - Base
baseurl=http://mirror.centos.org/centos/$releasever/os/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

[updates]
name=CentOS-$releasever - Updates
baseurl=http://mirror.centos.org/centos/$releasever/updates/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

[extras]
name=CentOS-$releasever - Extras
baseurl=http://mirror.centos.org/centos/$releasever/extras/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
```
换源  
`curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo ##CentOS 7`  

##### 常用 YUM 命令

| 命令 | 作用 |
| --- | --- |
| `yum install package` | 安装软件包 |
| `yum update package` | 更新软件包 |
| `yum remove package` | 卸载软件包 |
| `yum list` | 列出所有可用的软件包 |
| `yum search keyword` | 搜索软件包 |
| `yum info package` | 显示软件包信息 |
| `yum clean all` | 清理缓存 |

#### DNF

DNF (Dandified YUM) 是 YUM 的下一代版本，默认用于 Fedora 和 RHEL 8 及更高版本。它的主要特点包括：

- **性能提升**：相比 YUM，DNF 的性能更好，处理速度更快。
- **内存使用优化**：DNF 使用更少的内存，适合资源有限的系统。
- **改进的依赖解析**：DNF 使用更先进的算法来处理包依赖关系，减少冲突和错误。
- **插件支持**：与 YUM 类似，DNF 也支持插件，可以扩展其功能。

##### 常用 DNF 命令

| 命令 | 作用 |
| --- | --- |
| `dnf install package` | 安装软件包 |
| `dnf update package` | 更新软件包 |
| `dnf remove package` | 卸载软件包 |
| `dnf list` | 列出所有可用的软件包 |
| `dnf search keyword` | 搜索软件包 |
| `dnf info package` | 显示软件包信息 |
| `dnf clean all` | 清理缓存 |

### Debian系列

#### apt

**APT 包管理器**

APT (Advanced Package Tool) 是 Debian 和 Ubuntu 及其衍生发行版中使用的包管理器。它的主要特点包括：

- **依赖管理**：自动处理包依赖关系，简化软件安装和更新过程。
- **仓库支持**：支持多个仓库，可以从不同的源获取软件包。
- **易用性**：命令简单易用，适合新手和高级用户。

**APT 源配置文件**

APT 源配置文件通常位于 `/etc/apt/sources.list` 文件中，或者位于 `/etc/apt/sources.list.d/` 目录下的 `.list` 文件中。每个文件包含仓库的配置信息。

**APT 源配置文件示例**

以下是一个典型的 APT 源配置文件示例：

```plaintext
deb http://archive.ubuntu.com/ubuntu/ focal main restricted
deb http://archive.ubuntu.com/ubuntu/ focal-updates main restricted
deb http://archive.ubuntu.com/ubuntu/ focal universe
deb http://archive.ubuntu.com/ubuntu/ focal-updates universe
deb http://archive.ubuntu.com/ubuntu/ focal multiverse
deb http://archive.ubuntu.com/ubuntu/ focal-updates multiverse
deb http://archive.ubuntu.com/ubuntu/ focal-backports main restricted universe multiverse
deb http://security.ubuntu.com/ubuntu focal-security main restricted
deb http://security.ubuntu.com/ubuntu focal-security universe
deb http://security.ubuntu.com/ubuntu focal-security multiverse
```

##### 常用 APT 命令

| 命令 | 作用 |
| --- | --- |
| `apt update` | 更新软件包列表 |
| `apt upgrade` | 升级已安装的软件包 |
| `apt install package` | 安装软件包 |
| `apt remove package` | 卸载软件包 |
| `apt list` | 列出所有可用的软件包 |
| `apt search keyword` | 搜索软件包 |
| `apt show package` | 显示软件包信息 |
| `apt autoremove` | 自动删除不再需要的软件包 |
| `apt clean` | 清理本地缓存的包文件 |

## 进程管理工具

| 命令 | 作用 |
| --- | --- |
| `ps` | 显示进程信息 |
| `top` | 实时显示系统进程信息 |
| `htop` | `top` 命令的增强版，提供更友好的用户界面 |
| `kill` | 终止进程 |
| `pkill` | 根据名称终止进程 |
| `pgrep` | 根据名称查找进程 |
| `nice` | 启动进程并设置优先级 |
| `renice` | 调整正在运行的进程的优先级 |

## 任务管理工具

### 简单命令

| 命令 | 作用 |
| --- | --- |
| `&` | 加在一个命令的最后，可以把这个命令放在后台执行,如gftp& |
| `ctrl+z` | 可以将一个正在前台执行的命令放在后台，但是处于暂停状态，不可执行 |
| `ctrl+c` | 前台进程的中止 |
| `jobs` | 显示当前 shell 会话中所有的后台任务及其状态 |
| `bg` | 使一个在后台暂停的任务继续在后台运行 |
| `fg` | 将一个后台任务调到前台运行 |

## 文件管理工具

### ls

`ls [options] [files]`  
显示目录下的内容

常用参数：  
[-a] 显示所有文件，包括隐藏文件
[-l] 以长格式显示
[-R] 递归显示子目录内容

**长格式**
```bash
-rw-r--r-- 1 root root 337 Oct  4 11:31 /etc/hosts
```

每一项数据的意义
| 意义                | 命令中的样子               |
|---------------------|---------------------------|
| The file type       | -  eg: "-"表示文件，"d"表示文件夹 |
| The file permissions| rw-r--r--  eg：用户、组、其他|
| Number of hard links| 1                         |
| File owner          | root                      |
| File group          | root                      |
| File size           | 337                       |
| Date and Time       | Oct 4 11:31               |
| File name           | /etc/hosts                |

### less

`less [options] filename`
分页显示文件内容  

常用参数：
[-N] 显示行号  
[+F] 查看文件变化的内容，适合看日志文件

使用时命令
| 命令 | 作用                   |
|------|------------------------|
| 上,回车,e,j | 向前一行              |
| 下,y,k | 向后一行              |
| y    | 向后一行              |
| k    | 向后一行              |
| f    | 向前翻页              |
| g    | 向后翻页              |
| /    | 向前搜索              |
| ?    | 向后搜索              |
| n    | 重复之前的搜索        |
| N    | 重复之前的搜索，但反向|
| g    | 到第一行              |
| Ng   | 到第 N 行             |
| G    | 到最后一行            |
| P    | 到文件开始            |
| Np   | 到文件的 N%           |
| h    | 显示帮助              |
| q    | 退出                  |

**使用技巧**

ls /root | less 分页观看复杂的输出  

### head

`head [options] [files]`  
显示文件前十行（默认）内容，可同时显示多个文件  

参数：  
[-n]显示行数  
*tip:可以省略参数直接 -50 显示50行*  
[-c]显示字节数  

### tail

`tail [options] [files]`  
显示文件前十行（默认）内容，可同时显示多个文件  

参数：  
[-n]显示行数  
[-c]显示字节数  
[-f]监视文件更改  
Ctrl+C 中断监视  
[-F]重新创建文件时继续监视该文件  

### ln

**软连接和硬链接**
- 硬链接可以看作是文件的另一个名字，将多个名字链接向相同的 inode。同一文件系统或分区才能创建硬链接。一个文件可以有多个硬链接。  
- 软连接可以看作是windows中的快捷方式，是一种引用的文件类型。不同文件系统或分区也能创建软链接。  

`ln -s [options] fileToBeLinked linkedName`  
默认创建硬链接，[-s]用来创建软链接

[-f] 强制覆盖符号链接的目标路径

`unlink linkedName` 或 `remove linkedName` 删除链接

### chown

`chown [options] user[:group] file[s]`  
改变文件的所有者和组  

[-R] 递归更改子目录所有文件  
[-h] 如果包含软链接，使用它，更改符号链接本身的组所有权  

### chmod

`chmod [options] mode file[s]`  
`chmod [OPTIONS] [ugoa…][-+=]perms…[,…] FILE...`  
改变文件的权限  

**用户组参数属性说明**

| 参数 | 说明                               |
|------|------------------------------------|
| u    | The file owner.                    |
| g    | The users who are members of the group. |
| o    | All other users.                   |
| a    | All users, identical to ugo.       |

**权限参数说明**

| 参数 | 说明                                                                 |
|------|----------------------------------------------------------------------|
| -    | Removes the specified permissions.                                   |
| +    | Adds specified permissions.                                          |
| =    | Changes the current permissions to the specified permissions. If no permissions are specified after the = symbol, all permissions from the specified user class are removed. |

**数字参数**

当使用4位数字时，第一位数字具有以下含义：  

| 数字 | 含义                |
|------|---------------------|
| 4    | setuid              |
| 2    | setgid              |
| 1    | sticky              |
| 0    | no changes          |

其余三位：  

| 字母 | 含义                |
|------|---------------------|
| r    | read (4)            |
| w    | write (2)           |
| x    | execute (1)         |
| -    | no permissions (0)  |

### du

`du [options] [files]`  
查看磁盘使用量 diskUsage  

[-s] 全部加起来的使用量  
[-h] 人性化显示  
[--appart-size] 实际数据量  
[-c] 通配符查询  

## 文件系统管理工具

### 文件系统
文件系统是操作系统中用于组织和管理文件数据的一种机制。它提供了一种逻辑结构，用于在存储设备上存储、访问和管理文件。文件系统的出现是为了更好地组织和管理数据，使得用户可以方便地存储和访问文件。

在 Linux 系统中，存在一些标准目录，它们在文件系统中有着特定的用途和重要性。下面是一些常见的标准目录及其作用：

| 目录   | 作用 |
| ------ | ---- |
| `/`    | 根目录，是整个文件系统的顶级目录，包含了所有其他目录和文件。 |
| `/bin` | 存放系统可执行的基本命令，如 `ls`、`cp`、`mv` 等。这些命令在系统启动时就可用，独立于其他文件系统。 |
| `/boot`| 包含了 Linux 系统启动时所需的文件，如内核、引导加载程序和启动配置文件。 |
| `/dev` | 包含设备文件，用于与系统中的各种设备进行交互，如硬盘、键盘、鼠标等。 |
| `/etc` | 存放系统的配置文件，如网络配置、用户账户配置、服务配置等。这些配置文件对系统的正常运行至关重要。 |
| `/home`| 用户的家目录，每个用户在该目录下都有一个独立的子目录用于存放个人文件和设置。 |
| `/lib` 和 `/lib64` | 存放系统所需的共享库文件，这些库文件被系统中的程序共享使用。 |
| `/media` 和 `/mnt` | 用于挂载可移动介质（如 USB 设备、光盘等）和其他临时挂载点。 |
| `/opt` | 用于安装第三方软件和应用程序的可选目录。 |
| `/proc`| 虚拟文件系统，提供有关系统内核和运行进程的信息。 |
| `/root`| 超级用户（root）的家目录，与普通用户的家目录类似，但只有超级用户才能访问。 |
| `/run` | 存放系统运行时产生的临时文件，如进程 ID 文件和锁文件。 |
| `/sbin`| 包含系统管理员使用的系统管理命令，如 `ifconfig`、`fdisk` 等。这些命令通常需要具备超级用户权限才能运行。 |
| `/srv` | 存放服务相关的数据，如网站数据。 |
| `/sys` | 虚拟文件系统，提供有关系统硬件的信息。 |
| `/tmp` | 用于存放临时文件，系统重启时会自动清空该目录下的文件。 |
| `/usr` | 包含用户安装的应用程序、库文件和文档等，通常较大。 |
| `/var` | 存放经常变化的文件，如日志文件、缓存文件和邮件队列。 |

### df

`df [options] filesystem`  
显示文件系统的磁盘空间使用情况  

```bash
Filesystem     1K-blocks      Used Available Use% Mounted on
dev              8172848         0   8172848   0% /dev
run              8218640      1696   8216944   1% /run
/dev/nvme0n1p3 222284728 183057872  27865672  87% /
tmpfs            8218640    150256   8068384   2% /dev/shm
tmpfs            8218640         0   8218640   0% /sys/fs/cgroup
tmpfs            8218640        24   8218616   1% /tmp
/dev/nvme0n1p1    523248    107912    415336  21% /boot
/dev/sda1      480588496 172832632 283320260  38% /data
tmpfs            1643728        40   1643688   1% /run/user/1000
```

[-h] 人性化显示  
[-t] 显示类型/过滤指定类型  
[-i] 打印有关文件系统inode使用情况的信息

### mount

`mount -t [type] [device] [dir]`  
挂载文件系统到指定目录  

### fdisk

`fdisk [options] [files]`  
一个用于创建分区方案的命令行工具  

[-l] 列出分区  

### mkfs

`mkfs -t [fs type] [target device]`  
`mkfs.[fs type] [target device]`  
格式化选择的某个文件系统中的磁盘或分区 "make file system"  

### lsblk

`lsblk [options] [device(s)]`  
获取有关 Linux 系统上的驱动器和块设备的信息 "list block devices"  

[-a] 列出所有块设备，包括空设备和cdrom
[-f] 显示每个设备的文件系统信息  
[-m] 打印每个设备的权限  
[-o] 指定要在输出中显示的字段  

## 网络管理工具

### ip

`ip [ OPTIONS ] OBJECT { COMMAND | help }`  
配置网络接口的强大工具  

addr对象最常用的命令是：show、add和del  
对象有
- link (l) - Display and modify network interfaces.
- address (a) - Display and modify IP Addresses.
- route (r) - Display and alter the routing table.
- neigh (n) - Display and manipulate neighbor objects (ARP table).

`ip addr show`  

### dig

#### 输出说明

dig是一个命令行工具，用于查询DNS信息和解决DNS相关问题。

示例：  
`dig linux.org`  
输出结果：  
![alt text](assert/linux-basic-command_dig.png)

 输出的第一行打印安装的dig版本和查询的域名。第二行显示全局选项（默认情况下，只有cmd）。[+nocmd]可以不显示，得是第一个参数。
```bash
; <<>> DiG 9.13.3 <<>> linux.org
;; global options: +cmd
```

下一节包括有关从请求的机构（DNS服务器）接收的应答的技术细节。头部显示操作码（由dig执行的操作）和操作的状态。在本例中，状态为NOERROR，这意味着请求的授权机构在没有任何问题的情况下处理了查询。 [+nocomments]不显示。 
```bash
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 37159
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 2, ADDITIONAL: 5
```

“OPT”伪段仅在较新版本的dig实用程序中显示。[+noedns]不显示   
```bash
;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
```

在“QUESTION”部分中，`dig`显示了查询（问题）。默认情况下，dig请求A记录。[+nopquestion]  
```bash
;; QUESTION SECTION:
;linux.org.			IN	A
```

“答案”部分为我们提供了问题的答案。正如我们已经提到的，默认情况下，dig将请求A记录。在这里，我们可以看到域linux.org指向104.18.59.123IP地址。[+nosonwise]  
```bash
;; ANSWER SECTION:
linux.org.		300	IN	A	104.18.59.123
linux.org.		300	IN	A	104.18.58.123
```

“附加”部分为我们提供了有关权威部分中显示的权威DNS服务器的IP地址的信息。[+noadditional]  
```bash
;; ADDITIONAL SECTION:
lia.ns.cloudflare.com.	84354	IN	A	173.245.58.185
lia.ns.cloudflare.com.	170762	IN	AAAA	2400:cb00:2049:1::adf5:3ab9
mark.ns.cloudflare.com.	170734	IN	A	173.245.59.130
mark.ns.cloudflare.com.	170734	IN	AAAA	2400:cb00:2049:1::adf5:3b82
```

dig输出的最后一部分包括有关查询的统计信息。[+nostats]  
```bash
;; Query time: 58 msec
;; SERVER: 192.168.1.1#53(192.168.1.1)
;; WHEN: Fri Oct 12 11:46:46 CEST 2018
;; MSG SIZE  rcvd: 212
```

#### 使用 dig 查询域名

**常用形式：**  
`dig +nocmd [domain] [type] +noall +answer`  
type:
- a
- cname
- txt
- mx
- ns
- any

#### 反向 DNS 查询

使用[-x] , 查询 ip 地址对应的域名

`dig -x [ip] +noall +answer`

#### 批量查询

使用[-f]

`dig -f domains.txt +short`

#### dig 行为控制（.digrc File  .digrc文件）

dig命令的行为可以通过在${HOME}/.digrc文件中设置每个用户的选项来控制。  
例如，如果只想显示答案部分，请打开文本编辑器并创建以下~/.digrc文件：  
![alt text](assert/linux-basic-command_dig2.png)
+nocmd +noall +answer

## 网络传输工具

### curl

curl 是常用的命令行工具，用来请求 Web 服务器。它的名字就是客户端（client）的 URL 工具的意思。

#### 常用命令

| 命令 | 作用 |
| --- | --- |
| `curl http://example.com` | 发送 GET 请求到指定 URL |
| `curl -o file.txt http://example.com/file.txt` | 下载文件并保存为 `file.txt` |
| `curl -O http://example.com/file.txt` | 下载文件并使用原始文件名保存 |
| `curl -d "param1=value1&param2=value2" -X POST http://example.com` | 发送 POST 请求并附带数据 |
| `curl -H "Content-Type: application/json" -d '{"key":"value"}' -X POST http://example.com` | 发送带有 JSON 数据的 POST 请求 |
| `curl -u username:password http://example.com` | 使用基本身份验证发送请求 |
| `curl -b cookies.txt http://example.com` | 发送请求时附带 Cookies |
| `curl -c cookies.txt http://example.com` | 将服务器返回的 Cookies 保存到文件 |
| `curl -x http://proxyserver:port http://example.com` | 通过 HTTP 代理发送请求 |
| `curl -I http://example.com` | 发送 HEAD 请求，获取响应头信息 |

## 文本编辑器

### vim
- 显示行号 :set number!
- 删除当前行 dd
- 清空文件内容
    - gg		# 跳至文件首行
    - dG		# 删除光标所在行到末尾行内容，d删除，G跳转到文件末尾行

## 文本处理工具

### 正则表达式

| 元字符 | 意义                           | 举例       | 举例意义                          | 可匹配结果                       |
|--------|--------------------------------|------------|-----------------------------------|----------------------------------|
| ^      | 行开头                         | ^aa        | 以aa开头                          | aa aaa aa_ aa123 …               |
| $      | 行结尾                         | aa$        | 以aa结尾                          | aa 312aa …                       |
| ^$     | 空行                           |            |                                   |                                  |
| ^aa$   | 整行只有aa                     | ^a$        | 匹配只有a的行，aba也不行          | a                                |
| ?      | 前面的字符出现1次以下          | ab?        | 出现0次或1次，就是不确定的意思    | a ab                             |
| +      | 前面的字符出现1次以上          | ab+        | b出现1次以上                      | ab abb abbb ……                   |
| {}     | 指定前面的字符出现次数范围     | ab{2,}c    | b出现2次以上,{,5}这是5次以下      | abbc abbbc ……                    |
| *      | 前面的字符出现任意次           | ab*        | b出现0次或多次                    | a ab abb abbb ……                 |
| .      | 除换行符外任意一个字符         | gr.p       | gr后接一个任意字符然后是p         | grep grap gr@p gr1p ……           |
| .{}    | 指定任意字符出现次数           | ab.{2,4}   | b后面出现2到4个任意字符           | ab#$ ab123 ab!4rq ab…            |
| .*     | 代表任意个任意字符             |            |                                   | ……                               |
| |      | 或                             | a\|b       | 包含a或b                          |                                  |
| []     | 文字字符域，单个字符匹配       | [abc]      | 包含a、b、c任意一个，等同a\|b\|c  | awd _23rc bbb                    |
| [^]    | 取反，只要一行里有一个字符符合条件整行都会匹配 | [^abc] | 不包含abc中任意一个字符          | qwe a13 ……                       |
| \s     | 空白符(空格、tab)              | a\sb       | a和b之间有空白                    | a b、a    b                      |
| \<、\b | 单词开头                       | \<re       | 单词以re开头                      | remove reverse review ……         |
| \>、\b | 单词结尾                       | tion\>     | 单词以tion结尾                    | function revolution ……           |
| ()     | 实现多个字符分组               | f(oo)*     | oo可以出现任意次                  | f foo foooo ……                   |

### grep

`grep [options] parttern [files]`  
返回文件中符合格式的内容  
 Global search Regular Expression and Print out the line

[-v] 返回不符合的内容  
[-R] 递归（包括软链接）  
[-l] 只返回文件名  
[-i] 不区分大小写  
[-w] 匹配完整的单词，不再匹配单词内字符串  
[-n] 显示行号  
[-c] 计数  
[-o] 只匹配指定内容,输出也是指定内容  
[-A] 多显示匹配内容之后的n行 --after
[-B] 多显示匹配内容之前的n行 --before
[-C] 多显示匹配内容前后的n行 --center

### egrep

和 `grep -E` 相同

其主要是对正则表达式中增加了以下元字符：

1. | 表示或，例如 egrep ‘a|b’ 表示匹配a或b
2. + 表示一次或多次重复，例如 egrep ‘a+’ 表示匹配一个或多个a
3. ? 表示零次或一次重复，例如 egrep ‘a?’ 表示匹配零个或一个a
4. () 表示分组，例如 egrep ‘(ab)+’ 表示匹配ab的一个或多个重复
5. {} 表示出现次数，例如 egrep ‘a{3}’ 表示匹配a出现3次 

## 压缩和解压工具

### tar

### gzip

### bzip2

### zip

### unzip

## 系统信息和监控工具

| 命令 | 作用 |
| --- | --- |
| `uname` | 显示系统信息 |
| `hostnamectl` | 显示或设置系统的主机名 |
| `lsb_release` | 显示发行版信息 |
| `uptime` | 显示系统运行时间及负载 |
| `dmesg` | 显示系统启动信息及内核日志 |
| `free` | 显示内存使用情况 |
| `df` | 显示磁盘使用情况 |
| `du` | 显示目录或文件的磁盘使用情况 |
| `top` | 实时显示系统进程信息 |
| `htop` | `top` 命令的增强版，提供更友好的用户界面 |
| `ps` | 显示进程信息 |
| `lscpu` | 显示 CPU 架构信息 |
| `lsblk` | 列出所有块设备信息 |
| `lspci` | 列出所有 PCI 设备信息 |
| `lsusb` | 列出所有 USB 设备信息 |
| `dmidecode` | 显示系统硬件信息，包括 BIOS、内存、处理器等 |
| `dmidecode`| 显示系统硬件信息，包括 BIOS、内存、处理器等 |
| `hwinfo`   | 提供详细的硬件信息（需要安装） |
| `inxi`     | 提供系统和硬件信息的简洁报告（需要安装） |
| `sar -n DEV` | 查看网络情况 |

| 列名    | 含义                                                                 |
| ------- | -------------------------------------------------------------------- |
| PID     | 进程id                                                               |
| USER    | 进程所有者的用户名                                                   |
| PR      | 优先级                                                               |
| NI      | nice值。负值表示高优先级，正值表示低优先级                          |
| VIRT    | 进程使用的虚拟内存总量，单位kb。VIRT=SWAP+RES                        |
| RES     | 进程使用的、未被换出的物理内存大小，单位kb。RES=CODE+DATA            |
| SHR     | 共享内存大小，单位kb                                                 |
| S       | 进程状态。D=不可中断的睡眠状态 R=运行 S=睡眠 T=跟踪/停止 Z=僵尸进程 |
| %CPU    | 上次更新到现在的CPU时间占用百分比                                    |
| %MEM    | 进程使用的物理内存百分比                                             |
| TIME+   | 进程使用的CPU时间总计，单位1/100秒                                   |
| COMMAND | 命令名/命令行                                                        |

### 系统信息显示工具

neofetch  

## 服务管理工具

### System V
一种最早的 Linux 服务管理方式,使用/etc/init.d 下的脚本来管理服务。

service 命令就是管理 System V 类型服务的命令。它主要用于操作/etc/init.d下的脚本。

特点:

- 初始化脚本存放在`/etc/init.d`目录下
- 利用`/etc/init.d` 下的脚本来管理服务,例如 `/etc/init.d/httpd` 启动httpd服务
- service 命令用于管理这些服务,例如 `service httpd restart` 重启httpd服务
- 针对单个服务管理
- 启动速度较慢，顺序启动
常用命令：

| 命令 | 作用 |
| --- | --- |
| `service service start` | 启动指定的服务 |
| `service service stop` | 停止指定的服务 |
| `service service restart` | 重启指定的服务 |
| `service service reload` | 重新加载指定的服务配置 |
| `service service status` | 查看指定服务的状态和详细信息 |
| `service --status-all` | 列出所有正在运行的服务 |
| `chkconfig --list` | 列出所有已经注册的服务和它们的运行级别 |

### systemd

一种新的服务管理方式,使用 systemctl 命令来管理 systemd类型的服务。  

特点:
- 初始化脚本存放在 `/etc/systemd/system`目录下
- systemd unit 文件描述服务的各种属性
- systemctl 命令管理这些服务,例如 `systemctl restart httpd.service` 重启httpd服务
- 统一管理所有服务
- 较快，并行启动

常用命令：

| 命令 | 作用 |
| --- | --- |
| `systemctl start service` | 启动指定的服务 |
| `systemctl stop service` | 停止指定的服务 |
| `systemctl restart service` | 重启指定的服务 |
| `systemctl reload service` | 重新加载指定的服务配置 |
| `systemctl enable service` | 设置指定的服务为开机自启动 |
| `systemctl disable service` | 禁止指定的服务开机自启动 |
| `systemctl status service` | 查看指定服务的状态和详细信息 |
| `systemctl list-units --type=service` | 列出所有正在运行的服务 |
| `systemctl list-unit-files --type=service` | 列出所有已经注册的服务 |

## 服务

### ssh 服务


SSHD（SSH Daemon）是 SSH 服务的守护进程，负责处理传入的 SSH 连接请求。它通常在服务器上运行，监听指定端口（默认是 22），并处理客户端的连接请求。


SSHD 的配置文件通常位于 `/etc/ssh/sshd_config`  


ssh 的配置文件路径 `/etc/ssh/sshd_config`  
```
service ssh start   启动ssh
service ssh status  查看ssh服务是否正常运行

开机自动启动ssh服务
方法一：
sysv-rc-conf
sysv-rc-conf --list | grep ssh
sysv-rc-conf ssh on  //系统自动启动SSH服务
sysv-rc-conf ssh off  // 关闭系统自动启动SSH服务
方法二：
update-rc.d ssh enable  //系统自动启动SSH服务
update-rc.d ssh disabled // 关闭系统自动启动SSH服务
```

## softmare mirror

#### usage
```
vi hello.sh //create a sh script file
chmod a+x hello.sh
./hello.sh
```

### 删除编译软件
1. make uninstall 执行作者编写的卸载文件
2. build目录下，执行：```xargs rm < install_manifest.txt```
make install之后，build目录下会有一个install_mainfest.txt的文件, 记录了安装的所有内容及路径，
执行 xargs rm < install_manifest.txt 就可以了。
如果没有这个文件，可以自己重新make install，从log中过滤出install的安装路径信息，保存到unistall.txt中，再执行xargs rm < unistall.txt即可。








### mysql

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
    ```
    sudo systemctl start mysql.service
    sudo systemctl stop mysql.service
    sudo systemctl restart mysql.service
    sudo systemctl status mysql.service
    ```
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


### nginx
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


### other
update-rc.d和sysv-rc-conf 更新系统启动项的脚本

### problem
#### Processing triggers for man-db
解决方法：
The Processing triggers for man-db step is only executed if the file /var/lib/man-db/auto-update exists. This is an empty file with the sole purpose of controlling this behavior, so it can be safely removed to disable this time-consuming and arguably unnecessary process.

I personally disable this trigger on all of my systems. While the man-db cache is supposed to enhance the manual page system's speed and functionality, I have not experienced any noticeable performance degradation or functional problem after disabling the trigger.

# Windows


## 系统镜像

Windows 操作系统主要区分为 Ghost 系统和 MSDN 系统。

- Ghost 系统  
    Ghost 系统一般由个人或团队修改官方原版 Windows 操作系统而成，因为 Ghost 系统安装时间短，安装后可能默认已经激活，所以深受装机商们的喜爱。但 Ghost 系统可能会造成系统不稳定，网上各种 Ghost 系统可能存在后门、自带各种第三方软件、篡改浏览器主页等行为。Ghost 系统有利也有弊，Ghost 系统详细介绍请前往 https://baike.baidu.com/item/ghost系统/8452726 进行了解。  
- MSDN 系统 
    MSDN 的全称为 Microsoft Developer Network，意为《微软开发者网络》，是微软一个期刊产品，专门介绍各种编程技巧。  
    真正意义上的 MSDN 指的是 MSDN Subscription（MSDN 订阅）。这是一种付费订阅服务，可以将微软几乎所有可开发软件以开发为目的使用，包括各种操作系统和应用程序。  
    MSDN 系统为官方原版，由 MSDN 订阅者从微软 MSDN 订阅中心下载，因为 Windows 操作系统属于商业软件，所以安装后一般默认为未激活，需要使用有效的正版密钥激活。  

## Windows 权限管理

### 用户账户

#### 介绍

Windows的用户帐户是对计算机用户身份的识别，且本地用户帐户和密码信息是存储在本地计算机上的（即由：安全账户管理器【Security Accounts Manager】负责SAM（Security Accounts Manager）数据库的控制和维护。  
SAM数据库则是位于注册表的【计算机\HKEY_LOCAL_MACHINE\SAM\SAM】下，受到ACL保护），SAM文件在【C:\Windows\System32\config】路径下。SAM对应的进程：lsass.exe （Local Security Authority Process）。  
通过本地用户和组，可以为用户和组分配权利和权限，从而限制用户和组执行某些操作的能力。 不同的用户身份拥有不同的权限，每个用户包含一个名称和一个密码，用户帐户拥有唯一的安全标识符(Security Identifier，SID)。

#### 默认用户账户信息

| 默认用户账户 | 含义 | 说明 |
| --- | --- | --- |
| Administrator | 管理员用户 | 管理计算机(域)的内置帐户（默认禁用） |
| DefaultAccount | 默认账户 | 系统管理的用户帐户（默认禁用） |
| defaultuser0 | 默认用户 | （默认禁用） |
| Guest | 来宾用户 | 提供给访客人员使用（默认禁用） |
| WDAGUtilityAccount | Windows Defender用户 | 系统为 Windows Defender 应用程序防护方案管理和使用的用户帐户（默认禁用） |

#### 常用命令

| 序号 | 命令 | 命令说明 |
| --- | --- | --- |
| 1 | `net user` | 查看系统账户 |
| 2 | `net user Cm0001 123456 /add` | 创建用户：Cm0001，密码：123456 |
| 3 | `net user Cm0001 987654` | 修改用户 Cm0001 的密码为 987654 |
| 4 | `net user Cm0001` | 查看用户 Cm0001 的属性 |
| 5 | `net localgroup administrators Cm0001 /add` | 提升用户 Cm0001 的权限为管理员 |
| 6 | `net user Cm0001 /del` | 删除用户 Cm0001 |

### 组账户

#### 介绍

组账户是一些用户的集合；且组内的用户自动拥有组所设置的权限。
- 组账户是用户账户的集合，用于组织用户账户
- 为一个组授予权限后，则该组内的所有成员用户自动获得改组的权限
- 一个用户账户可以隶属于多个组，而这个用户的权限就是所有组的权限的合并集

#### 内置组账户

| 组账户名称 | 含义 | 说明 |
| --- | --- | --- |
| Administrators | 管理员组 | 默认情况下，Administrators 组中的用户对计算机/域有不受限制的完全访问权。功能包括：<br>① 管理文件：系统磁盘中的文件只能由 Administrators 组的账户进行更改。<br>② 更改系统安全设置：安装新功能、更改计算机网络设置、对服务器选项进行设置等操作需要 Administrators 组中的用户进行操作。<br>默认情况下，Administrator 账户处于禁用状态。当启用时，具有对计算机的完全控制权限，并根据需要向用户分配权力和访问控制权限。建议设置强密码，不可从管理员组删除，但可以重命名或禁用。 |
| Guests | 来宾用户组 | 提供给没有用户帐户但需要访问本地计算机资源的用户使用。该组的成员无法永久改变其桌面的工作环境，最常见的默认成员为 Guest。<br>① 通常没有修改系统设置和安装程序的权限。<br>② 没有创建或修改任何文档的权限，只能读取系统信息和文件。<br>③ 默认情况下禁用 Guest 用户，且此账户默认为 Guests 组成员，其他权限需由管理员组中的用户成员赋予。 |
| Power Users | 功能用户组 | 组内用户具备比 Users 组更多的权利，但比 Administrators 组少。例如，可以创建、删除、更改本地用户帐户；管理本地计算机内的共享文件夹与共享打印机；自定义系统设置等。<br>① 不可以更改 Administrators。<br>② 无法夺取文件的所有权。<br>③ 无法备份与还原文件。<br>④ 无法安装或删除设备驱动程序。<br>⑤ 无法管理安全与审核日志。 |
| Users | 标准用户组 | 权限低于 Administrators 组，但高于 Guests 组。<br>① 可以进入“网络和共享中心”并查看网络连接状态，但无法修改连接属性。<br>② 无法关闭防火墙。<br>③ 无法安装软件。<br>④ 无法对该用户文件夹以外的 C 盘进行修改。 |
| Remote Desktop Users | 远程桌面用户组 | 组内成员拥有远程桌面登录的权限；默认 Administrators 组内的成员都拥有远程桌面的权限。<br>Remote Desktop Users 组的作用是保障远程桌面服务的安全运行。将需要连接远程桌面的用户分到 Remote Desktop Users 组中是一种更安全的方式。 |

#### 常用命令

| 序号 | 组命令 | 说明 |
| --- | --- | --- |
| 1 | `net localgroup` | 查看系统的组 |
| 2 | `net localgroup testgroup /add` | 新建一个 testgroup 的组 |
| 3 | `net localgroup testgroup Cm0001 /add` | 将用户 Cm0001 加入 testgroup 组中 |
| 4 | `net localgroup testgroup` | 查看 testgroup 组内的成员 |
| 5 | `net localgroup testgroup Cm0001 /del` | 将用户 Cm0001 从 testgroup 组中移除 |
| 6 | `net localgroup testgroup /del` | 删除 testgroup 组 |
| 7 | `net localgroup "remote desktop users" hack /add` | 将用户 hack 加入 remote desktop users 组中 |
| 8 | `net localgroup "remote desktop users"` | 查看 remote desktop users 组内的成员 |
| 9 | `net localgroup "remote desktop users" hack /del` | 将用户 hack 从 remote desktop users 组中移除 |

### 访问控制

当一个用户试图访问一个文件或者文件夹的时候，NTFS 文件系统会检查用户使用的帐户或者账户所属的组是否在此文件或文件夹的访问控制列表（ACL）中。如果存在，则进一步检查访问控制项 ACE，然后根据控制项中的权限来判断用户最终的权限  

![alt text](Windows/image.png)

| 访问控制名称 | 含义 | 说明 |
| --- | --- | --- |
| Access Control List | 访问控制列表(ACL) | 访问权限决定着某个用户可以访问的文件和目录。对于每一个文件和文件夹，由安全描述符(SD)规定了安全数据。安全描述符决定安全设置是否对当前目录有效，或者它可以被传递给其他文件和目录。 |
| Access Control environment | 访问控制环境（ACE） | 访问控制项ACE，是指访问控制实体，用于指定特定用户/组的访问权限，是权限控制的最小单位。<br>① 完全控制：对文件或者文件夹可执行所有操作；<br>② 修改：可以修改、删除文件或文件夹；<br>③ 读取和执行：可以读取内容，并且可以执行应用程序；<br>④ 列出文件夹目录：可以列出文件夹内容，此权限只针对文件夹存在，文件无此权限；<br>⑤ 读取：可以读取文件或文件夹的内容；<br>⑥ 写入：可以创建文件或文件夹；<br>⑦ 特别的权限：其他不常用的权限，比如删除权限的权限； |
| New Technology File System | 文件系统（NTFS） | 文件夹的NTFS权限 (文件夹内的文件或文件夹会默认继承上一级目录的权限)。<br>① 完全控制：对文件或者文件夹可执行所有操作；<br>② 修改：可以修改、删除文件或文件夹；<br>③ 读取和执行：可以读取内容，并且可以执行应用程序；<br>④ 读取：可以读取文件的内容；<br>⑤ 写入：可以修改文件的内容；<br>⑥ 特殊权限：其他不常用的权限，比如删除权限的权限； |
| Security Identifiers | 安全标识符（SID） | SID的说明：<br>安全标识符是标识用户、组和计算机帐户的唯一的号码。在第一次创建该帐户时，将给网络上的每一个帐户发布一个唯一的 SID。Windows 2000 中的内部进程将引用帐户的 SID 而不是帐户的用户或组名。如果创建帐户，再删除帐户，然后使用相同的用户名创建另一个帐户，则新帐户将不具有授权给前一个帐户的权力或权限，原因是该帐户具有不同的 SID 号。安全标识符也被称为安全 ID 或 SID。<br>SID的作用：<br>用户通过验证后，登陆进程会给用户一个访问令牌，该令牌相当于用户访问系统资源的票证，当用户试图访问系统资源时，将访问令牌提供给 Windows NT，然后 Windows NT 检查用户试图访问对象上的访问控制列表。如果用户被允许访问该对象，Windows NT将会分配给用户适当的访问权限。访问令牌是用户在通过验证的时候有登陆进程所提供的，所以改变用户的权限需要注销后重新登陆，重新获取访问令牌。 |


## shift + del 强制删除文件

# Andriod

## 玩机软件
shizuku
scene

# drawin

苹果开源系统
