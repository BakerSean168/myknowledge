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

# 外设

## 键盘

### 薄膜键盘

### 机械键盘

键帽、轴体、套件

#### 配列

百分比或键数表示，数字越大，按键越多  
104  

客制化  
Alice(人体工学)  

##### 键帽

PBT  更耐磨、触感偏硬，表层颗粒大
ABS  触感亲肤温润、时间长打油
PC  透光性好

刻字工艺  
- 二色成型
- 热升华

高度  
- SA  
- MDA  
- OEM  
- 原厂
![alt text](AAA_PictureDir_装机/键盘高度.png)

##### 轴体

线性轴、段落轴、发声段落轴

其他参数  
- 轴体压力  
   一般为 45 g  
- 导通行程  
   按压到触发的距离，标准为 2 mm，  
- 总键程  
   按压到触底的距离，一般 3.6 mm  

#### 套件

##### 外壳材质  

- 塑料  
- 铝  
   铝合金处理工艺
   - 喷涂
   - 阳极氧化
   - 电泳

![alt text](AAA_PictureDir_装机/铝外壳处理手感区别.png)

##### 定位板

- PC
- POM
- FR4
- 铝
- 碳纤维
- 铜

![alt text](AAA_PictureDir_装机/定位板材质对手感音色的影响.png)

##### 内部结构

船壳结构  早期、成本低、容易共振
Gasket 结构  主流
TOP 结构  手感扎实
三明治结构  

##### PCB

热插拔 PCB 自由换轴体  
焊接 PCB

### 磁轴键盘

### 产品

- VGN V87
    有线/无线/蓝牙三模客制化机械键盘  
    gasket 结构  
    全键热插拔  
    动力银轴  
    加勒比海  
    电池容量 4000mAh（连接电脑充电 6h，无线开灯续航 20h，关灯 20 天）  

## 鼠标

### 组成和参数

- 传感器  
   3395  
- 模具  
   握姿 + 手长  
   [鼠标模具查看网站](www.eloshapes.com)

- 回报率  
   回报率也被称为轮询率或者刷新率（FPS），通常是指鼠标向计算机报告其位置的频率，单位为 Hz（赫兹）。比如一个鼠标回报率是 125 Hz，那么它每秒会向计算机报告其位置125次。理论上来说，回报率越高，操作鼠标时的延迟就会越低，鼠标移动也就更丝滑。  
   不过太高的回报率也会消耗更多的CPU资源，特别是无线鼠标，建议调低回报率增加续航时间。  

### 价格

0 - 200 性能足够  
200 - 400 性能顶尖  
400 - ∞ 创新独特  

## 鼠标垫

- 布垫  
   顺滑度较好、价格较便宜  
   比较容易脏  
   推荐带锁边  
- 皮革垫  
   相比布垫，抗污性更强、质感颜色更好  
   阻力较大；只有纯色；长期沾有会油亮，不好清理  
   推荐带缝线  
- 毛毡垫  
   质感好  
   抗污能力差；阻力大；几个月会起球  
- 玻璃垫  
   顺滑；抗污；  
   冰手；贵  

## 显示器

- 色域
- 色准
- 面板
- 背光
- 硬件防蓝光
- 对比度

### 显示器类型

1. **CRT（Cathode Ray Tube）显示器**：
   - 使用阴极射线管技术。
   - 体积大、重量重，但色彩表现和响应速度较好。
   - 逐渐被淘汰，取而代之的是更轻薄的显示技术。

2. **LCD（Liquid Crystal Display）显示器**：
   - 使用液晶技术，通过背光源照射液晶层来显示图像。
   - 轻薄、能耗低，广泛应用于各种设备。
   - 分为 TN、IPS、VA 等不同面板类型。

3. **LED（Light Emitting Diode）显示器**：
   - 实际上是 LCD 显示器的一种，使用 LED 作为背光源。
   - 亮度高、能耗低、寿命长。
   - 常见于现代显示器和电视。

4. **OLED（Organic Light Emitting Diode）显示器**：
   - 使用有机发光二极管技术，每个像素自发光。
   - 对比度高、色彩表现优秀、响应速度快。
   - 价格较高，主要用于高端设备。

5. **QLED（Quantum Dot LED）显示器**：
   - 使用量子点技术增强色彩表现。
   - 亮度高、色域广，主要用于高端电视和显示器。

### 分辨率

- **分辨率**：显示器屏幕上像素的数量，通常表示为宽度 x 高度（例如 1920x1080）。
- **常见分辨率**：
  - HD（720p）：1280x720
  - Full HD（1080p）：1920x1080
  - QHD（1440p）：2560x1440
  - 4K UHD：3840x2160
  - 8K UHD：7680x4320

### 刷新率

- **刷新率**：显示器每秒刷新图像的次数，以赫兹（Hz）为单位。
- **常见刷新率**：
  - 60Hz：标准刷新率，适用于大多数日常使用。
  - 120Hz、144Hz、240Hz：高刷新率，适用于游戏和专业应用，提供更流畅的视觉体验。

### 响应时间

- **响应时间**：像素从一种颜色转换到另一种颜色所需的时间，以毫秒（ms）为单位。
- **低响应时间**：减少运动模糊和拖影，适合快速移动的图像，如游戏和视频。

### 面板类型

1. **TN（Twisted Nematic）面板**：
   - 响应时间快、成本低。
   - 色彩表现和可视角度较差。

2. **IPS（In-Plane Switching）面板**：
   - 色彩准确、可视角度广。
   - 响应时间较慢、成本较高。

3. **VA（Vertical Alignment）面板**：
   - 对比度高、色彩表现好。
   - 响应时间介于 TN 和 IPS 之间。

### 护眼

德国莱茵认证

#### 硬件防蓝光

#### 调光模式

##### PWN

会频闪

##### DC

大多使用，对双眼较好

### 连接接口

- **DVI（Digital Visual Interface）**：较老的数字视频接口，逐渐被 HDMI 和 DisplayPort 取代。
- **VGA（Video Graphics Array）**：模拟视频接口，逐渐被数字接口取代。
- **HDMI（High-Definition Multimedia Interface）**：常见的数字视频和音频接口，广泛应用于显示器、电视和其他设备。
- **DP（DisplayPort）**：高性能数字接口，支持高分辨率和高刷新率，常用于电脑显示器。

![alt text](AAA_PictureDir_装机/显示器HDMI与DP支持的分辨率刷新率.png)

### 其他特性

- **色域**：显示器能够显示的颜色范围，常见的色域标准有 sRGB、Adobe RGB 和 DCI-P3。
- **HDR（High Dynamic Range）**：高动态范围技术，提供更高的亮度和对比度，提升图像质量。
- **G-Sync 和 FreeSync**：同步技术，减少屏幕撕裂和卡顿，提升游戏体验。

#### 独显直连

独立显卡不经过核显直接输出到显示器，渲染画面

##### 效果

网游普遍吃cpu，关闭核显就是降低cpu的一份功耗和热量来提升cpu性能，直接用独显渲染画面帧数就会提示非常多。  
单机普遍吃显卡，尤其是显存。作为市面上最多的60系列显卡，除4060外几乎都是6g以内的显存，这个时候核显是可以共享显存的，否则显卡容易爆显存。  

HDMI
    2.0 支持 2k 144Hz  
    2.1 支持 2k 180Hz
DP（推荐）

# Test

图片
![image](data:image/png;base64,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)

图片