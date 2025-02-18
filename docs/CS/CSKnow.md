### 寻址方式

```
为了缩短指令中某个地址段的位数，有效的方法是采取寄存器寻址。
单地址指令中为了完成两个数的算术操作，除地址码指明的一个操作数外，另一个数常需采用隐含寻址方式。
零地址运算指令在指令格式中不给出操作数地址，因此它的操作数来自栈顶和次栈顶。
指令系统中采用不同寻址方式的目的主要是缩短指令长度，扩大寻址空间，提高编程灵活性。
基址寻址方式中，操作数的有效地址是基址寄存器内容加上形式地址（位移量）。
采用变址寻址可扩大寻址范围，且变址寄存器内容由用户确定，在程序执行过程中可变。
便于处理数组的寻址方式为变址寻址
在一地址格式的指令中，可能有一个操作数，也可能有两个操作数
变址寻址和基址寻址的有效地址形成方式类似，但是在程序执行过程中，基址寄存器的内容不可变，变址寄存器中的内容可变

```

## 存储器

![alt text](AAA_PictureDir_CSKnow/image.png)

| 存储器类型                             | 说明                                                                                       | 特点                                                              | 用途                                                                                                                    |
|-----------------------------------|------------------------------------------------------------------------------------------|-----------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| SRAM（Static Random Access Memory） | SRAM 是静态随机存取存储器，它使用双稳态触发器（如触发器）来存储每一位数据。由于每个存储单元由多个晶体管组成，SRAM 不需要像 DRAM 那样定期刷新数据，因此速度较快。 | -速度快：由于不需要刷新，SRAM 的访问速度比 DRAM 快。 <br>-功耗低：在不进行读写操作时，SRAM 的功耗较低。 | -高速缓存（Cache）：SRAM 常用于 CPU 的一级缓存（L1 Cache）、二级缓存（L2 Cache）和三级缓存（L3 Cache）。<br>-嵌入式系统：由于其速度快和功耗低，SRAM 也常用于嵌入式系统中的高速存储需求。 |
| DRAM（Dynamic Random Access Memory） | DRAM 是动态随机存取存储器，它使用电容来存储每一位数据。由于电容会漏电，DRAM 需要定期刷新数据以保持其内容，因此速度较慢。 | -速度较慢：由于需要定期刷新，DRAM 的访问速度比 SRAM 慢。 <br>-功耗较高：刷新操作需要消耗额外的功率，因此 DRAM 的功耗较高。 <br>-集成度高：每个存储单元只需要一个电容和一个晶体管，因此 DRAM 的集成度较高，单位面积内的存储容量较大。 <br>-成本低：由于使用了较少的晶体管，DRAM 的制造成本较低。 | -主存储器（Main Memory）：DRAM 常用于计算机的主存储器（RAM），如 DDR SDRAM、DDR2、DDR3、DDR4 等。<br>-图形存储器（Graphics Memory）：DRAM 也常用于图形处理器（GPU）的显存（VRAM）。 |

### Cache

#### 直接映射

#### 四路组相联

#### 全相联映射

### 外存

CPU不能直接访问的

#### 固态硬盘（Solid State Drive-SSD）

[B站视频地址](https://www.bilibili.com/video/BV1XW4y187Nc/?spm_id_from=333.337.search-card.all.click&vd_source=15c229538881316b8c6a43f997de056f)

是一种基于闪存技术的存储设备，与传统的机械硬盘（HDD）相比，具有更高的性能和可靠性。  

![alt text](AAA_PictureDir_CSKnow/image-1.png)  

##### 原理

闪存技术：SSD 使用 NAND 闪存芯片来存储数据。每个 NAND 闪存芯片包含多个存储单元，每个单元可以存储一个或多个比特的数据。  
控制器：SSD 内部有一个控制器，用于管理数据的读写操作、错误校正、垃圾回收等功能。  

##### 参数

###### 类型

| 数据协议 | 描述 |
|----------|------|
| SATA     | 串行高级技术附件（Serial ATA），一种常见的硬盘接口协议，广泛用于消费级 SSD 和 HDD。 |
| NVMe     | 非易失性存储器快速（Non-Volatile Memory Express），一种高性能协议，专为 SSD 设计，利用 PCIe 通道。 |
| AHCI     | 高级主机控制器接口（Advanced Host Controller Interface），一种用于 SATA 接口的协议，支持传统 HDD 和 SSD。 |

| 数据协议通道 | 描述 |
|---------------|------|
| PCIe          | 外设组件互连快（Peripheral Component Interconnect Express），一种高速接口，支持 NVMe 协议，提供高带宽和低延迟。 |
| SATA          | 串行高级技术附件（Serial ATA），一种常见的硬盘接口，支持 AHCI 协议，适用于传统 HDD 和 SSD。 |
| SAS           | 串行连接 SCSI（Serial Attached SCSI），一种企业级接口，提供高性能和高可靠性，适用于服务器和数据中心。 |

| 接口类型 | 描述 |
|----------|------|
| PCIe     | 高速接口，直接连接到主板上的 PCIe 插槽，支持 NVMe 协议，适用于高性能存储设备。目前已经很少见了 |
| SATA     | 常见的硬盘接口，适用于大多数台式机和笔记本电脑。 |
| M.2      | 一种小型化接口，支持 SATA 和 NVMe 协议，适用于超薄笔记本电脑和高性能台式机。 |
| U.2      | 一种企业级接口，支持 NVMe 协议，提供高性能和高可靠性。 |

![alt text](AAA_PictureDir_CSKnow/image-2.png)  
![alt text](AAA_PictureDir_CSKnow/image-3.png)  

###### 颗粒

| 颗粒类型                   | 容量 | 速度 | 寿命（擦写次数）   | 优点           | 消费场景  |
|------------------------|----|----|------------|--------------|-------|---|---|
| SLC(Single-Level Cell) | 1  | 16 | 1 万~10 万   | 速度快、寿命长、可靠性高 | 企业级   |
| MLC(Multi-Level Cell)  | 4  | 8  | 5000~10000 | 成本适中、容量适中    | 高端消费级 |
| TLC(Triple-Level Cell) | 8  | 4  | 1000~3000  | 成本低、容量大      | 一般消费级 |
| QLC(Quad-Level Cell)   | 16 | 1  | 几百~1000    | 成本最低、容量最大    | 还不推荐  |

![alt text](AAA_PictureDir_CSKnow/image-4.png)

##### 主控

大部分主控都具有平衡磨损、垃圾回收、地址映射等功能。无缓的主控还有SLC模拟和HMB缓存技术。部分主控还有数据恢复功能。  

![alt text](AAA_PictureDir_CSKnow/image-6.png)  

##### 缓存

独立缓存  
是 DRAM 缓存，使用内存芯片，用于存放 FTL 映射表（索引目录），加快查找速度。  
中高端才有独立缓存  
没有独立缓存的 FTL 映射表直接放在缓冲颗粒里，或者利用内存条  

模拟缓存  
固态硬盘必备  
快速的数据中转仓，用于提升固态的数据处理速度  
把固态硬盘当作模拟缓存，当固态空间减少，模拟缓存减少，速度就会变慢  
![alt text](AAA_PictureDir_CSKnow/image-7.png)  


##### 4k 随机读写

固态硬盘远强于机械硬盘之处  

极大提升电脑流畅度  

##### TBW 数据写入量

![alt text](AAA_PictureDir_CSKnow/image-5.png)

## IO 设备

键盘、鼠标

## 指令集架构

### RISC（精简指令集计算机）

RISC 设计的一个目标是使大多数指令在一个时钟周期内完成，以提高执行效率。

RISC 处理器通常具有更多的内部通用寄存器，以减少对内存的访问，提高性能。

RISC 的设计原则之一是简化指令集，因此 RISC 的指令数、寻址方式和指令格式种类相对 CISC（复杂指令集计算机）少。

### CISC

## 处理器型号

### x86

早期，1980s年代，x86一般指当时的处理器8088和80286，不过这两个处理器都是16位的。如今，x86通常指32位指令集架构的处理器，比如80386。80386处理器是intel在1985年实现的第一款32位指令集架构的处理器，又叫i386，Intel Architecture, 32-bit，缩写为IA-32，现在，IA-32一般又能引喻成所有的支持32位计算的x86架构。

按照发展历史看，x86应该是指令集概念，一般用于个人PC系统如8086,286,386。IA-32是intel首推的32位架构。

### x86-64/x64/amd64/Intel64

在1999年，AMD公司首先在IA-32基础上，增加了64位寄存器，兼容早期的16位和32位软件系统，推出了x86-64的64位微处理器，后来命名为AMD64，实现了超车。然后intel公司也接受了该方案，叫做Intel64。x86-64应该只算是x86指令集的64位扩展，并不是一种全新的64位架构。

由于amd64和intel64本质上是一样的，叫法也是很多。AMD通常叫它x86-64、x86_64，微软和sun等软件公司叫它x64，操作系统厂商则通常用AMD64或者amd64来指代AMD64和Intel64。

### IA-64

IA-64是Intel推出的用于Itanium处理器（安腾处理器）的自己的Intel Architecture 64位指令集，一般用于服务器。尽管Intel64也是64位处理器，但这两者完全不是一回事。IA-64软件不能直接运行于Intel64处理器上。x86-64是IA-32指令集的扩展，而IA-64则是完完全全没有一点IA-32影子的独立处理器架构。IA-64需要通过模拟器才能运行IA-32，但是性能大大受影响。

### 市面上处理器如何区分AMD64和IA-64呢？

市面上买的Intel 64-bit的cpu其实都属于amd64分类，intel64和amd64其实都应该叫做x86_64。  
IA64则指Itaniums系统cpu，并不是x86架构的，一般都是用于服务器，不是个人桌面产品，价格昂贵。  
ARM64/AArch64  
ARM是精简指令集RISC下的处理器架构。ARMv3至ARMv7支持32位寻址空间。ARMv8-A开始支持64位寻址空间。AArch64和ARM64都是指64位的ARM架构。  

### 外接设置


# 计算机操作系统
