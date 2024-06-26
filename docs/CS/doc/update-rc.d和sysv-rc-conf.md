 系统启动：运行级别，/etc/init.d，rcconf，update-rc.d
https://learnku.com/docs/linux-the-hard-way/ex15/6217

首先我会给出一个典型的系统启动过程的概述：

你
    按电源开关（或启动虚拟机）
    现在计算机获得控制权
    控制权传给了 BIOS
BIOS
    执行硬件特定的任务
    执行开机自检（POST），测试你的硬件
    检测安装的硬件，如硬盘，内存类型和数量，...
    通过将初始值写入其内存来初始化硬件
    找到一个启动设备，通常是一个硬盘
    读取并执行位于此磁盘开头的 MBR（主引导记录）
    控制权现在传给了 MBR
MBR
    MBR 寻找并执行 GRUB（多重操作系统启动管理器）
    控制权现在传给了 GRUB
GRUB
    查找可用的文件系统
    查找并读取其配置文件，来了解：
        系统位于哪里
        启动什么系统
        执行什么其他的操作
    执行 Linux 内核，Linux 操作系统的主要部分
    控制权现在传给了 Linux 内核
Linux 内核
    查找并加载 initrd，这是初始的 ram 磁盘
        initrd 包含必要驱动程序，允许真实文件系统的访问和挂载
    挂载文件系统，它在 GRUB 配置文件中指定。
    执行`/sbin/init`，一个启动所有其他程序的特殊程序
    控制权现在传给了 init
init
    查看`etc/inittab`来确定所需的运行级别
    加载适合此运行级别的所有程序
        加载来自`/etc/rc.d/rc2.d/`的所有程序，因为 2 是默认的 Debian 运行级别
        启动 SSH 和 TTY，以便你可以连接到你的计算机
    启动现在完成了
你
    使用 SSH 连接到你的计算机
    SSH 守护进程为你执行 bash shell
    你现在可以输入东西
    你再次获得控制权
现在我们只对 “init” 和 “运行级别” 阶段感兴趣，所以我将总结一下，系统如何启动并自动启动一些程序。首先，有一些术语​​：

守护进程 - 一直运行在后台的程序。这意味着它不在乎你是否登录系统，通常你不需要手动启动它，因为它在计算机启动时自动启动。
运行级别 - 系统运行模式。基本上，这只是一个数字，提供给 init 程序，它知道哪些守护程序与每个数字相关联，并根据需要启动并停止这些守护程序。
在 Debian 中有以下运行级别：

ID	描述
S	系统通电后会执行它
0	停止，这定义了当系统关闭时执行哪些操作。
1	单用户模式，这是一种特殊的故障排除模式。在这种模式下，大多数守护进程不会自动启动。
2~5	完全多用户，配置的守护程序在此模式下启动。
6	重启，类似停止，但不是关闭系统而是重新启动。
但是 init 怎么知道的？好吧，这是用于它的特殊目录。

user1@vm1:/etc$ find /etc -type d -name 'rc*' 2>/dev/null | sort
/etc/rc0.d
/etc/rc1.d
/etc/rc2.d
/etc/rc3.d
/etc/rc4.d
/etc/rc5.d
/etc/rc6.d
/etc/rcS.d
你可能能猜到，每个数字和 S 对应表中的运行级别。让我们列出其中一个目录，它在正常启动中启动所有所需的守护进程。

user1@vm1:/etc$ ls -al /etc/rc2.d | awk '{printf "%-15.15s %-3.3s %s\n",$9,$10,$11}'
.
..
README
S14portmap      ->  ../init.d/portmap
S15nfs-common   ->  ../init.d/nfs-common
S17rsyslog      ->  ../init.d/rsyslog
S17sudo         ->  ../init.d/sudo
S18acpid        ->  ../init.d/acpid
S18atd          ->  ../init.d/atd
S18cron         ->  ../init.d/cron
S18exim4        ->  ../init.d/exim4
S18ssh          ->  ../init.d/ssh
S20bootlogs     ->  ../init.d/bootlogs
S21rc.local     ->  ../init.d/rc.local
S21rmnologin    ->  ../init.d/rmnologin
S21stop-bootlog ->  ../init.d/stop-bootlogd
如你所见，此目录中的文件只是实际启动脚本的符号链接。我们来看看其中一个链接：S18ssh→../init.d/ssh。这是关于这个文件的事情：

它是一个./init.d/ssh 文件的链接
它以 S 开始，意味着 “启动”。Debian 启动系统中使用的每个脚本至少有 2 个参数，“启动” 和 “停止”。现在我们可以说，当我们的系统切换到运行级别 2 时，该脚本将使用动作 “启动” 来执行 。
它有一个数字 18。rc 目录中的脚本以字典序执行，所以现在我们明白，在启动 ssh 之前 ，系统启动 portmap，nfs-common，rsyslog 和 sudo。rsyslog 是一个系统日志守护程序，特别是 ssh 想要记录谁在什么时候访问系统，所以在启动之前需要运行 rsyslog。
现在，你将学习如何列出启用的服务（守护程序），以及启用和禁用服务（守护程序）。

这样做
 1: sudo aptitude install rcconf
 2: ls -al /etc/rc2.d
 3: sudo rcconf --list
 4: sudo update-rc.d exim4 disable
 5: ls -al /etc/rc2.d
 6: sudo rcconf --list
 7: sudo update-rc.d exim4 enable
 8: ls -al /etc/rc2.d
 9: sudo rcconf --list
你会看到什么
user1@vm1:/var/log$ sudo aptitude install rcconf
The following NEW packages will be installed:
  rcconf
0 packages upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 0 B/23.9 kB of archives. After unpacking 135 kB will be used.
Selecting previously deselected package rcconf.
(Reading database ... 24239 files and directories currently installed.)
Unpacking rcconf (from .../archives/rcconf_2.5_all.deb) ...
Processing triggers for man-db ...
Setting up rcconf (2.5) ...

user1@vm1:/etc$ ls -al /etc/rc2.d
total 12
drwxr-xr-x  2 root root 4096 Jun 27 11:42 .
drwxr-xr-x 68 root root 4096 Jun 25 18:43 ..
-rw-r--r--  1 root root  677 Mar 27 05:50 README
lrwxrwxrwx  1 root root   17 Jun  4 11:53 S14portmap -> ../init.d/portmap
lrwxrwxrwx  1 root root   20 Jun  4 11:53 S15nfs-common -> ../init.d/nfs-common
lrwxrwxrwx  1 root root   17 Jun  4 11:53 S17rsyslog -> ../init.d/rsyslog
lrwxrwxrwx  1 root root   14 Jun 15 19:02 S17sudo -> ../init.d/sudo
lrwxrwxrwx  1 root root   15 Jun  4 11:53 S18acpid -> ../init.d/acpid
lrwxrwxrwx  1 root root   13 Jun  4 11:53 S18atd -> ../init.d/atd
lrwxrwxrwx  1 root root   14 Jun  4 11:53 S18cron -> ../init.d/cron
lrwxrwxrwx  1 root root   15 Jun 27 11:42 S18exim4 -> ../init.d/exim4
lrwxrwxrwx  1 root root   13 Jun  4 11:53 S18ssh -> ../init.d/ssh
lrwxrwxrwx  1 root root   18 Jun  4 11:53 S20bootlogs -> ../init.d/bootlogs
lrwxrwxrwx  1 root root   18 Jun  4 11:53 S21rc.local -> ../init.d/rc.local
lrwxrwxrwx  1 root root   19 Jun  4 11:53 S21rmnologin -> ../init.d/rmnologin
lrwxrwxrwx  1 root root   23 Jun  4 11:53 S21stop-bootlogd -> ../init.d/stop-bootlogd
user1@vm1:/etc$ sudo rcconf --list
rsyslog on
ssh on
bootlogs on
portmap on
sudo on
nfs-common on
udev on
console-setup on
kbd on
exim4 on
keyboard-setup on
acpid on
cron on
atd on
procps on
module-init-tools on
user1@vm1:/etc$ sudo update-rc.d exim4 disable
update-rc.d: using dependency based boot sequencing
insserv: warning: current start runlevel(s) (empty) of script `exim4' overwrites defaults (2 3 4 5).
insserv: warning: current stop runlevel(s) (0 1 2 3 4 5 6) of script `exim4' overwrites defaults (0 1 6).
user1@vm1:/etc$ ls -al /etc/rc2.d
total 12
drwxr-xr-x  2 root root 4096 Jun 27 11:43 .
drwxr-xr-x 68 root root 4096 Jun 25 18:43 ..
lrwxrwxrwx  1 root root   15 Jun 27 11:43 K01exim4 -> ../init.d/exim4
-rw-r--r--  1 root root  677 Mar 27 05:50 README
lrwxrwxrwx  1 root root   17 Jun  4 11:53 S14portmap -> ../init.d/portmap
lrwxrwxrwx  1 root root   20 Jun  4 11:53 S15nfs-common -> ../init.d/nfs-common
lrwxrwxrwx  1 root root   17 Jun  4 11:53 S17rsyslog -> ../init.d/rsyslog
lrwxrwxrwx  1 root root   14 Jun 15 19:02 S17sudo -> ../init.d/sudo
lrwxrwxrwx  1 root root   15 Jun  4 11:53 S18acpid -> ../init.d/acpid
lrwxrwxrwx  1 root root   13 Jun  4 11:53 S18atd -> ../init.d/atd
lrwxrwxrwx  1 root root   14 Jun  4 11:53 S18cron -> ../init.d/cron
lrwxrwxrwx  1 root root   13 Jun  4 11:53 S18ssh -> ../init.d/ssh
lrwxrwxrwx  1 root root   18 Jun  4 11:53 S20bootlogs -> ../init.d/bootlogs
lrwxrwxrwx  1 root root   18 Jun  4 11:53 S21rc.local -> ../init.d/rc.local
lrwxrwxrwx  1 root root   19 Jun  4 11:53 S21rmnologin -> ../init.d/rmnologin
lrwxrwxrwx  1 root root   23 Jun  4 11:53 S21stop-bootlogd -> ../init.d/stop-bootlogd
user1@vm1:/etc$ sudo rcconf --list
rsyslog on
ssh on
bootlogs on
portmap on
sudo on
nfs-common on
udev on
console-setup on
kbd on
keyboard-setup on
acpid on
cron on
atd on
procps on
module-init-tools on
exim4 off
user1@vm1:/etc$ sudo update-rc.d exim4 enable
update-rc.d: using dependency based boot sequencing
user1@vm1:/etc$ ls -al /etc/rc2.d
total 12
drwxr-xr-x  2 root root 4096 Jun 27 11:43 .
drwxr-xr-x 68 root root 4096 Jun 25 18:43 ..
-rw-r--r--  1 root root  677 Mar 27 05:50 README
lrwxrwxrwx  1 root root   17 Jun  4 11:53 S14portmap -> ../init.d/portmap
lrwxrwxrwx  1 root root   20 Jun  4 11:53 S15nfs-common -> ../init.d/nfs-common
lrwxrwxrwx  1 root root   17 Jun  4 11:53 S17rsyslog -> ../init.d/rsyslog
lrwxrwxrwx  1 root root   14 Jun 15 19:02 S17sudo -> ../init.d/sudo
lrwxrwxrwx  1 root root   15 Jun  4 11:53 S18acpid -> ../init.d/acpid
lrwxrwxrwx  1 root root   13 Jun  4 11:53 S18atd -> ../init.d/atd
lrwxrwxrwx  1 root root   14 Jun  4 11:53 S18cron -> ../init.d/cron
lrwxrwxrwx  1 root root   15 Jun 27 11:43 S18exim4 -> ../init.d/exim4
lrwxrwxrwx  1 root root   13 Jun  4 11:53 S18ssh -> ../init.d/ssh
lrwxrwxrwx  1 root root   18 Jun  4 11:53 S20bootlogs -> ../init.d/bootlogs
lrwxrwxrwx  1 root root   18 Jun  4 11:53 S21rc.local -> ../init.d/rc.local
lrwxrwxrwx  1 root root   19 Jun  4 11:53 S21rmnologin -> ../init.d/rmnologin
lrwxrwxrwx  1 root root   23 Jun  4 11:53 S21stop-bootlogd -> ../init.d/stop-bootlogd
user1@vm1:/etc$ sudo rcconf --list
rsyslog on
ssh on
bootlogs on
portmap on
sudo on
nfs-common on
udev on
console-setup on
kbd on
exim4 on
keyboard-setup on
acpid on
cron on
atd on
procps on
module-init-tools on
user1@vm1:/etc$
解释
安装 rcconf 包，让你轻松管理运行级别。
打印包含运行级别 2 的启动脚本的目录。现在启用了邮件服务器 exim4。
仅仅打印出相同运行级别的服务。请注意，由于它们被视为系统服务，因此存在多个未显示的服务。rcconf –list –expert 会把它们全部列出，以及更多的驻留在不同的运行级别上的服务。
禁用邮件服务器 exim4 的自动启动。
打印出包括运行级别 2 的启动脚本的目录。exim4 启动脚本现在从 S18exim4 重命名为 K01exim4。这意味着 exim4 进入此级别时已停止（被杀死）。如果 exim4 开始没有运行，就没有任何反应。
打印运行级别 2 的服务。服务 exim4 现在已关闭。
开启 exim4 的自动启动。
再次打印包含运行级别 2 的启动脚本的目录，exim4 再次启动。
打印运行级别 2 的服务。exim4 的状态变更为已启动，和预期一样。
