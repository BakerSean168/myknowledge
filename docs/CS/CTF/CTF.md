# Web|网络攻防

## HTTP协议

请求方式  
302跳转  
Cookie  
基础认证  
响应包源代码  

## 信息泄露

目录遍历  
PHPINFO  

备份文件下载  
网站源码  
bak文件  会在修改某个文件的时候先复制一份，将其命名为xxx.bak
vim缓存  vim缓存文件第一次生成.swp文件  
.DS_Store  DS_Store是MacOS保存文件夹的自定义属性的隐藏文件。通过.DS_Store可以知道这个目录里面所有文件的清单。  

Git泄露  
SVN泄露  
HG泄露  

## 密码口令

弱口令  
字典爆破  
默认口令  
社会工程  

## SQL注入

整数型注入  
字符型注入  
报错注入  
布尔盲注  
时间盲注  
MySQL结构  
Cookie注入  
UA注入  
Refer注入  
二次注入  
Where后注入  
AND/OR注入  
ORDER BY 注入  
UPDATE注入  
INSERT注入  
过滤空格  
综合训练 SQLI-LABS  

## XSS

反射型  
存储型  
DOM反射  
DOM跳转  
过滤空格  
过滤关键词  

## 文件上传

无验证  
前端验证  
.htaccess  
MIME绕过  
00截断  
后缀大小写绕过  
点绕过  
空格绕过  
双写后缀  
文件头检查  
突破getimagesize()  
突破exif_imagetype()  
二次渲染  

## RCE

无过滤执行  
过滤空格
eval执行
文件包含
php://input  
读取源代码
远程包含
命令注入
过滤cat  
过滤空格
过滤目录分隔符
过滤运算符
综合过滤练习  

## SSRF

内网访问  
伪协议读取文件  
端口扫描  

POST请求  
上传文件  
FastCGI协议  
Redis协议  
  
URL Bypass  
数字IP Bypass    
302跳转 Bypass  
DNS重绑定 Bypass    

# Crypto|密码学

## 介绍

````
密码学（英语：Cryptography）可分为古典密码学和现代密码学。在西方语文中，密码学一词源于希腊语 kryptós“隐藏的”，和*gráphein*“书写”。古典密码学主要关注资讯的保密书写和传递，以及与其相对应的破译方法。而现代密码学不只关注资讯保密问题，还同时涉及资讯完整性验证（消息验证码）、资讯发布的不可抵赖性（数码签名）、以及在分布式计算中产生的来源于内部和外部的攻击的所有信息安全问题。

—— 中文 wiki- 密码学
````

对 「编码 Encoding 」 的解释如下：

````
    In cryptology, a code is a method used to encrypt a message that operates at the level of meaning; that is, words or phrases are converted into something else. A code might transform "change" into "CVGDK" or "cocktail lounge". The U.S. National Security Agency defined a code as "A substitution cryptosystem in which the plaintext elements are primarily words, phrases, or sentences, and the code equivalents (called "code groups") typically consist of letters or digits (or both) in otherwise meaningless combinations of identical length."[1]: Vol I, p. 12  A codebook is needed to encrypt, and decrypt the phrases or words.

    —— 英文 wiki- 编码 (密码学)
````

这里国内外存在一些差异，在中文 wiki 上这样写着：

````
    编码：它意指以码字取代特定的明文。例如，以‘苹果派’（apple pie）替换‘拂晓攻击’（attack at dawn）。编码已经不再被使用在严谨的密码学，它在资讯论或通讯原理上有更明确的意义
````

虽然不再符合现代 严谨的密码学 的定义，但在广义的密码学上 「编码 Encoding 」 依旧被承认为密码学分支，同时编码在现代密码学信息承载上依旧有巨大作用。

## 工具

### CyberChef

[CyberChef](https://github.com/gchq/CyberChef "Github地址") 是 CTF 中最常用的编码解码工具之一，内含多种编码和解码方式。  

### Ciphey

[Ciphey](https://github.com/Ciphey/Ciphey  "Github地址") is a Fully automated decryption/decoding/cracking tool using natural language processing & artificial intelligence, along with some common sense.  

### 随波逐流

[随波逐流 CTF 编码工具](http://1o1o.xyz/bo_ctfcode.html) 由随波逐编写开发，CTF 编码工具为用户提供丰富的离线符编码进行转换，加密解密功能。

## 常见编码

ASCLL  
HEx  
URL  
BASE  
摩斯密码  

# Misc

## 信息收集

## 编码扩展

## 文件基础

## 压缩包

## 隐写技术

## 流量分析

## 内存取证

# Reverse|逆向工程

## 介绍

````
对已经编译完成的 可执行文件 进行分析，通过反汇编工具查看程序的二进制代码，以及汇编块，研究程序的行为和算法，然后以此为依据，得出出题人想隐藏的 flag。
````

关键字:
````
题型:Windows 逆向、Linux 逆向和 Android 逆向，再加上 Flash 逆向、Python 逆向、.NET 逆向、ARM 逆向等
题目常见形式: ELF 文件、exe 文件、dll 文件等
加密方法出现：混淆、花指令、加壳、复杂算法、复杂汇编等
````

## 可执行文件

在 Linux 环境下，其主要的可执行文件对应的名称为 ELF（Executable and Linking Format）文件  
在 Windows 环境下，其可执行文件对应的名称为 PE（Portable Executable）文件。  

### ELF

ELF 文件标准里把系统中采用 ELF 格式的文件分为以下四种：
- 可重定位文件（Relocatable File），这类文件包含代码和数据，可用来连接成可执行文件或共享目标文件，静态链接库归为此类，对应于 Linux 中的 .o ，Windows 的 .obj。
- 可执行文件（Executable File），这类文件包含了可以直接执行的程序，它的代表就是 ELF 可执行文件，他们一般没有扩展名。比如 .bin .bash，以及 Windows 下的 .exe。
- 共享目标文件（Shared Object File），这种文件包含代码和数据，链接器可以使用这种文件跟其他可重定位文件的共享目标文件链接，产生新的目标文件。另外是动态链接器可以将几个这种共享目标文件与可执行文件结合，作为进程映像来运行。对应于 Linux 中的 .so，Windows 中的 .dll。
- 核心转储文件（Core Dump File），当进程意外终止，系统可以将该进程地址空间的内容及终止时的一些信息转存到核心转储文件。 对应 Linux 下的 core dump。


#### ELF 文件结构

| 部分 | 含义 |
| --- | --- |
| ELF Header | ELF 文件头，包含文件类型、架构、入口点地址等信息。 |
| .text | 代码段，包含程序的可执行指令。 |
| .data | 数据段，包含已初始化的全局变量和静态变量。 |
| .bss | 未初始化数据段，包含未初始化的全局变量和静态变量。 |
| Other Section ... | 其他段，如.rdata 表示这里存储只读数据，.debug 表示调试信息。 |
| Section Header Table | 段头表，描述每个段的位置和属性。 |
| String Tables | 字符串表，包含符号名和其他字符串。 |

#### 区段名称及其作用

| 名称 | 类型 | 属性 | 含义 |
| --- | --- | --- | --- |
| .bss | SHT_NOBITS | SHF_ALLOC + SHF_WRITE | 包含将出现在程序的内存映像中的未初始化数据。根据定义，当程序开始执行，系统将把这些数据初始化为 0。此节区不占用文件空间。 |
| .comment | SHT_PROGBITS | (无) | 包含版本控制信息。 |
| .data | SHT_PROGBITS | SHF_ALLOC + SHF_WRITE | 包含初始化了的数据，将出现在程序的内存映像中。 |
| .data1 | SHT_PROGBITS | SHF_ALLOC + SHF_WRITE | 包含初始化了的数据，将出现在程序的内存映像中。 |
| .debug | SHT_PROGBITS | (无) | 包含用于符号调试的信息。 |
| .dynamic | SHT_DYNAMIC | SHF_ALLOC | 包含动态链接信息。节区的属性将包含 SHF_ALLOC 位。是否 SHF_WRITE 位被设置取决于处理器。 |
| .dynstr | SHT_STRTAB | SHF_ALLOC | 包含用于动态链接的字符串，大多数情况下这些字符串代表了与符号表项相关的名称。 |
| .dynsym | SHT_DYNSYM | SHF_ALLOC | 包含了动态链接符号表。 |
| .fini | SHT_PROGBITS | SHF_ALLOC + SHF_EXECINSTR | 包含了可执行的指令，是进程终止代码的一部分。程序正常退出时，系统将安排执行这里的代码。 |
| .got | SHT_PROGBITS | (无) | 包含全局偏移表。 |
| .hash | SHT_HASH | SHF_ALLOC | 包含了一个符号哈希表。 |
| .init | SHT_PROGBITS | SHF_ALLOC + SHF_EXECINSTR | 包含了可执行指令，是进程初始化代码的一部分。当程序开始执行时，系统要在开始调用主程序入口之前（通常指 C 语言的 main 函数）执行这些代码。 |
| .interp | SHT_PROGBITS | (无) | 包含程序解释器的路径名。如果程序包含一个可加载的段，段中包含此节区，那么节区的属性将包含 SHF_ALLOC 位，否则该位为 0。 |
| .line | SHT_PROGBITS | (无) | 包含符号调试的行号信息，其中描述了源程序与机器指令之间的对应关系。其内容是未定义的。 |
| .note | SHT_NOTE | (无) | 包含注释信息，有独立的格式。 |
| .plt | SHT_PROGBITS | (无) | 包含过程链接表（procedure linkage table）。 |
| .relname .relaname | SHT_REL SHT_RELA | (无) | 包含了重定位信息。如果文件中包含可加载的段，段中有重定位内容，节区的属性将包含 SHF_ALLOC 位，否则该位置 0。传统上 name 根据重定位所适用的节区给定。例如 .text 节区的重定位节区名字将是：.rel.text 或者 .rela.text。 |
| .rodata .rodata1 | SHT_PROGBITS | SHF_ALLOC | 包含只读数据，这些数据通常参与进程映像的不可写段。 |
| .shstrtab | SHT_STRTAB | (无) | 包含节区名称。 |
| .strtab | SHT_STRTAB | (无) | 包含字符串，通常是代表与符号表项相关的名称。如果文件拥有一个可加载的段，段中包含符号串表，节区的属性将包含 SHF_ALLOC 位，否则该位为 0。 |
| .symtab | SHT_SYMTAB | (无) | 包含一个符号表。如果文件中包含一个可加载的段，并且该段中包含符号表，那么节区的属性中包含 SHF_ALLOC 位，否则该位置为 0。 |
| .text | SHT_PROGBITS | SHF_ALLOC + SHF_EXECINSTR | 包含程序的可执行指令。 |

### PE

| 名称 | 描述 |
| --- | --- |
| Image File | 镜像文件：包含以 EXE 文件为代表的可执行文件、以 DLL 文件为代表的动态链接库。因为它们常常被直接“复制”到内存中执行，有“镜像”的某种意思。 |
| Section | 节：是 PE 文件中代码或数据的基本单元。原则上讲，节只分为“代码节”和“数据节”。 |
| VA | 基址：英文全称 Virtual Address。即为在内存中的地址。 |
| RVA | 相对基址偏移：英文全称 Relatively Virtual Address。偏移（相对虚拟地址）。相对镜像基址的偏移。 |

#### 文件结构

![alt text](CTF/p2-1.png)

DOS 头：是用来兼容 MS-DOS 操作系统的，目的是当这个文件在 MS-DOS 上运行时提示一段文字，大部分情况下是：This program cannot be run in DOS mode. 还有一个目的，就是指明 NT 头在文件中的位置。

NT 头：包含 windows PE 文件的主要信息，其中包括一个 'PE' 字样的签名，PE 文件头 (IMAGE_FILE_HEADER) 和 PE 可选头 (IMAGE_OPTIONAL_HEADER32)。

节表：是 PE 文件后续节的描述，Windows 根据节表的描述加载每个节。

节：每个节实际上是一个容器，可以包含代码、数据 等等，每个节可以有独立的内存权限，比如代码节默认有读 / 执行权限，节的名字和数量可以自己定义，未必是上图中的三个。

# Pwn|二进制安全

# AWD|攻防模式

# AI|人工智能安全

# blockchain|区块链安全

# 理论知识

## 信息安全基础知识

## 法律法规及安全标准