# Assembly

**OFFSET**
取得其后变量或标号的偏移地址

**SEG**
取得其变量或标号的段地址

**PTR**
指定其后存储器操作数的类型
- MOV BYTE PTR[BX], 12H

**LEA**
lea，官方解释Load Effective Address，即装入有效地址的意思，它的操作数就是地址；

常见的几种用法：
1. lea eax，[addr]
就是将表达式addr的值放入eax寄存器，示例如下：
lea eax,[401000h]; 将值401000h写入eax寄存器中
lea指令右边的操作数表示一个精指针，上述指令和mov eax，401000h是等价的
2. lea eax，dword ptr [ebx];将ebx的值赋值给eax
3. lea eax，c；其中c为一个int型的变量，该条语句的意思是把c的地址赋值给eax；

**SAL and SAR**
算术移位指令
SAL：每次移动时，SAL 都将目的操作数中的每一位移动到下一个最高位上。最低位用 0 填充；最高位移入进位标志位，该标志位原来的值被丢弃

SAR：首位（符号位）不变，并且右移，最低位进入标志位
下面的例子展示了 SAR 是如何复制符号位的。执行指令前 AL 的符号位为负，执行指令后该位移动到右边的位上：
mov al, 0F0h ; AL = 11110000b (-16)
sar al, 1     ; AL = 11111000b (-8) , CF = 0

**SHL and SHR**
(Shift Logical Left) and (Shift Logical Right)
逻辑移位指令

功能：空位补0，最高位进入CF

**RCL and RCR**
(Rotate Left Through Carry)
带进位的循环移位指令

功能：最高位进CF后进最低位

**标号**
地址标号：仅仅表示地址
数据标号：标记了存储数据的单元的地址和长度//不加冒号

**ADC and add**
ADD 两数相加，不加进位位。 ADDC 两数相加，加进位位

**DEBUG**
*用R命令查看、改变CPU寄存器的内容*
-R -查看寄存器内容
-R寄存器名 -改变指定寄存器内容
*用D命令查看内存中的内容*
-D  -列出预设地址内存储的128个字节的内容
-D 段地址：偏移地址 -列出内存中指定地址处的内容
-D 段地址：偏移地址 结尾偏移地址 -列出内存中指定地址处的内容
*用E命令改变内存中的内容*
-E 段地址：偏移地址 数据1 2 ……
-E 段地址：偏移地址  //逐个询问时修改
*用U命令将内存中的机器指令翻译成汇编指令*
-U 段地址：偏移地址
*用A命令以汇编指令的格式在内存中写入机器指令*
-A 段地址：偏移地址
*用T命令执行机器指令*
-T - 执行CS：IP处的指令
*用Q命令退出Debug*


**CPU从内存单元中读取数据**
![alt text](img/assimg-8.png)

**stack**
在8086CPU中有两个和栈有关的寄存器
- 栈段寄存器ss -存放栈顶的段地址
- 栈顶指针寄存器sp -存放栈顶的偏移地址
![alt text](img/assimg-9.png)

**汇编语言程序的工作过程**
![alt text](img/assimg-10.png)

**三种伪指令**
![alt text](img/assimg-11.png)

**如何写一个程序**
![alt text](img/assimg-12.png)

**loop指令**
![alt text](img/assimg-13.png)

**段前缀**
![alt text](img/assimg-14.png)

**字符**
汇编程序中用''的方式指明字符，编译器将他们转化为ASCLL码

**内存寻址方式**
![alt text](img/assimg-15.png)

**div指令**
![alt text](img/assimg-16.png)

**dup指令**
![alt text](img/assimg-17.png)

**test**
Test命令将两个操作数进行逻辑与运算，并根据运算结果设置相关的标志位。但是，Test命令的两个操作数不会被改变。运算结果在设置过相关标记位后会被丢弃。

**DAA(Decimal Adjust After Addition)**
组合(压缩)BCD码的加法调整指令。
格式：DAA
功能：将AL的内容调整为两位组合型的二进制数。调整方法与AAA指令类似，不同的是DAA指令要分别考虑AL的高4位和低4位。
如果AL的低4位大于9或AF=1，则AL的内容加06H，并将AF置1；

如果AL的高4位大于9或CF=1，则AL的内容加60H，且将CF置1。



**DAS（Decimal Adjust for Subtraction）**
组合(压缩)BCD码的加法调整指令。
格式：DAS
功能：
如果AL低四位>9或AF=1 ，则AL的值减06h，并置AF=1
如果AL高四位>9或CF=1 ，则AL的值减60h ,且置CF=1


## 转移
![alt text](img/assimg-18.png)

**offset操作符**
offset作用：取得标号的偏移地址
格式：
    offset 标号
例子：
    start： move ax，offset start；相当于 move ax，0

**jmp指令**
![alt text](img/assimg-7.png)
jmp short 标号 -短转移，位移为8位，范围-128~127
jmp near ptr 标号 -近转移，位移为16位，范围-32769~32767
jmp far ptr 标号 -远转移
*短转移和近转移给定偏移量，而远转移直接给定偏移地址*

**jcxz**
原理：
jmp改
作用：
如果（cx）=0，则跳转到标号处执行；否则什么也不做（程序向下执行）
格式：
jcxz 标号

**条件转移指令**
![alt text](image.png)

**call**
原理：
1. 将当前的IP或CS和IP压入栈中；
2. 转移到标号处执行指令。
*近转移*
作用：
调用子程序
格式：
call 标号

**call far ptr**
原理：
push CS
push IP
jmp far ptr 标号
    
**mul**
作用：
乘法指令
格式：
mul 寄存器
mul 内存单元

**cmp**
原理：
对象1-对象2，通过其他指令识别标志寄存器变化来得知比较结果
作用：
比较指令
格式：
cmp 对象1，对象2

**串传送指令**
movsb：（以字节为单位传送）
movsw：（以字为单位传送）

**移位指令**
![alt text](img/assimg-21.png)

**操作显存数据**
低位字节：要显示符号的ascll
高位字节：
| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|
|BL | R | G | B | I | R | G | B |
|闪烁|背景|||高亮|前景|||

## 中断
中断：CPU不再向下执行指令，而去处理中断信息
内中断：CPU内部发生的事件而引起的中断
外中断：外部设备发生的事件引起的中断


## 与外设交互

**读写端口指令**
in： CPU从端口读取数据
执行时：
1. CPU通过**地址总线**将地址信息60h发出；
2. CPU通过**控制线**发出端口读命令，选中端口所在的芯片，并通知要从中读取数据；
3. 端口所在的芯片将60h端口中的数据通过**数据总线**送入CPU。
out： CPU从端口写入数据

**PC机键盘处理过程**
1. **键盘输入**：键盘中的每一个按键相当于一个开关，键盘中有一个芯片来监控这些开关
    1. 键盘被按下：
        - 开关接通，芯片产生一个扫描码，记录闭合开关的位置
        - 扫描码被送入主板相关接口芯片的寄存器（端口位置为60H）中
    2. 键盘被松开：
        - 同上
    3. 扫描码：长度为一个字节的编码
        - 按下产生的扫描码--通码，第七位为0
        - 松开产生的扫描码--断码，第七位为1
2. **引发9号中断**
3. **执行int 9中断例程**

---

# C

## 编译器

GCC、Clang、Microsoft C++、Intel C++、Borland C++、IBM XLC、Digital Mars、Cygwin、MinGW 和 DJGPP

### MSVC

MSVC是微软Windows平台Visual Studio自带的C/C++编译器。

优点：对Windows平台支持好，编译快。

缺点：对C++的新标准支持得少。

### MinGW

### GCC

GCC原名GNU C Compiler，后来逐渐支持更多的语言编译（C++、Fortran、Pascal、Objective-C、Java、Ada、Go等），所以变成了GNU Compiler Collection（GNU编译器套装），是一套由GNU工程开发的支持多种编程语言的编译器。GCC是自由软件发展过程中的著名例子，由自由软件基金会以GPL协议发布，是大多数类Unix（如Linux、BSD、Mac OS X等）的标准编译器，而且适用于Windows（借助其他移植项目实现的，比如MingW、Cygwin等）。GCC支持多种计算机体系芯片，如x86、ARM，并已移植到其他多种硬件平台。

优点：类Unix下的标准编译器，支持众多语言，支持交叉编译。

缺点：默认不支持Windows，需要第三方移植才可用于Windows。

### Clang

基于 LLVM 的编译器，编译速度快，错误信息友好，模块化设计易于扩展，但某些优化不如 GCC。

---

# Java

## java读取文件数据

### Scanner

1. 适用于逐行读取文件内容。
2. 提供了更灵活的输入解析功能，如读取整数、浮点数等。
3. 适合处理文本文件。
4. 可以自定义分隔符

以下是以“|”为分隔符，读取 int 类型数据的代码

```java
fileName = "text.txt";
//内容 1|2
try (Scanner sc = new Scanner (new FileReader(fileName))) {
    sc.useDelimiter("\\|"); //分隔符
    while (sc.hasNextInt()) {
        int intValue = sc.nextINt();
        System.out.println(intValue);
    }
}
```

### Files.lines

1. 返回Stream流式数据处理
2. 适用于逐行读取文件内容。
3. 使用Java 8的Stream API，提供了强大的流处理功能。
4. 适合处理大文件，因为它是惰性读取的，不会一次性将整个文件读入内存。

```java
String fileName = "text.txt";

Stream<String> lines = Files.lines(Path.get(fileName));
lines.forEach(System.out::println);
lines.forEachOrdered(System.out::println);
//内容 1|2

```

### Files.readAllLines

1. 返回List<String>
2. 适用于一次性读取整个文件内容。
3. 读取效率较高，但对于大文件可能会占用较多内存。
4. 适合处理小到中等大小的文本文件。

```java
List<String> lines = Files.lines(Path.get(fileName));
lines.forEach(System.out::println);

```

### Files.readSrting

1. 读取String
2. 文件最大2G

```java
String s = FIles.readString(Paths.get(fileName));
```

### Files.readAllBytes

1. 读取byte[]
2. 文件最大2G

```java
byte[] bytes = Files.readAllBytes(Paths.get(fileName));
String content = new String(bytes, StandardCharsets.UTF_8);
System.out.println(content);
```

### BufferedRead
1. 缓冲区默认8k，适合读取较大文件
2. 适用于逐行读取文件内容。
3. 使用缓冲机制，读取效率较高。
4. 适合处理文本文件

```java
tyr (BufferedReader br = new BufferedReader(new FileReader(fileName))) {
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
}
```

### RandomAccessFile
1. 适用于需要随机访问文件内容的场景。
2. 可以读取和写入文件的任意位置。
3. 适合处理需要频繁读写的文件。

```java
try (RandomAccessFile file = new RandomAccessFile(fileName, "r")) {
    String line;
    while ((line = file.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

## java集合框架

collection

Java集合框架为程序员提供了预先包装的数据结构和算法来操纵他们。
集合是一个对象，可容纳其他对象的引用。集合接口声明对每一种类型的集合可以执行的操作。
集合框架的类和接口均在java.util包中。
任何对象加入集合类后，自动转变为Object类型，所以在取出的时候，需要进行强制类型转换。

### 比较器

Comparator

```java
// 按到达时间排序
Collections.sort(processes, new Comparator<Process>() {
    @Override
    public int compare(Process p1, Process p2) {
        return Double.compare(p1.arrivalTime, p2.arrivalTime);
    }
});
```


### 命名规范
**包命名规范**
包(Package)的作用是将功能相似或相关的类或者接口进行分组管理，便于类的定位和查找，同时也可以使用包来避免类名的冲突和访问控制，使代码更容易维护。通常，包命使用小写英文字母进行命名，并使用“.”进行分割，每个被分割的单元只能包含一个名词。

一般地，包命名常采用顶级域名作为前缀，例如com，net，org，edu，gov，cn，io等，随后紧跟公司/组织/个人名称以及功能模块名称。

**类命名规范**
类(Class)通常采用名词进行命名，且首字母大写，如果一个类名包含两个以上名词，建议使用驼峰命名(Camel-Case)法书写类名,每个名词首字母也应该大写。一般地，类名的书写尽量使其保持简单和描述的完整性，因此在书写类名时不建议使用缩写(一些约定俗成的命名除外。

例如 Internationalization and Localization 缩写成i18n，Uniform Resource Identifier缩写成URI，Data Access Object缩写成DAO，JSON Web Token缩写成JWT，HyperText Markup Language缩写成HTML等等)。

https://blog.csdn.net/cxyxysam/article/details/136218734

### ==

8大类型（String,Integer,Long,Byte,Boolean等）  

==比较的是内存地址,equal比较的是值  
```
String str1 = new String("Hello");  
String str2 = new String("Hello");  
str1 == str2 // false  
str1.equals(str2) // true  
```

### break

break只能跳出与之最近的for，while循环，跟if没有关系。

# CSS

## position

[position](https://developer.mozilla.org/zh-CN/docs/Web/CSS/position)

position — 作为css属性三巨头（position、display、float）之一，它的作用是用来决定元素在文档中的定位方式。其属性值有五种，分别是  
- static（正常定位）  
    该关键字指定元素使用正常的布局行为，即元素在文档常规流中当前的布局位置。此时 top, right, bottom, left 和 z-index 属性无效。  
- relative（相对定位）  
    该关键字下，元素先放置在未添加定位时的位置，再在不改变页面布局的前提下调整元素位置（因此会在此元素未添加定位时所在位置留下空白）。position:relative 对 table-*-group, table-row, table-column, table-cell, table-caption 元素无效。  
- absolute（绝对定位）  
    元素会被移出正常文档流，并不为元素预留空间，通过指定元素相对于最近的非 static 定位祖先元素的偏移，来确定元素位置。绝对定位的元素可以设置外边距（margins），且不会与其他边距合并。
- fixed（固定定位）  
    元素会被移出正常文档流，并不为元素预留空间，而是通过指定元素相对于屏幕视口（viewport）的位置来指定元素位置。元素的位置在屏幕滚动时不会改变。打印时，元素会出现在的每页的固定位置。fixed 属性会创建新的层叠上下文。当元素祖先的 transform、perspective、filter 或 backdrop-filter 属性非 none 时，容器由视口改为该祖先。  
    固定定位与绝对定位相似，但元素的包含块为 viewport 视口。该定位方式常用于创建在滚动屏幕时仍固定在相同位置的元素。  
- sticky（粘性定位）  
    元素根据正常文档流进行定位，然后相对它的最近滚动祖先（nearest scrolling ancestor）和 containing block（最近块级祖先 nearest block-level ancestor），包括 table-related 元素，基于 top、right、bottom 和 left 的值进行偏移。偏移值不会影响任何其他元素的位置。 该值总是创建一个新的层叠上下文（stacking context）。注意，一个 sticky 元素会“固定”在离它最近的一个拥有“滚动机制”的祖先上（当该祖先的 overflow 是 hidden、scroll、auto 或 overlay 时），即便这个祖先不是最近的真实可滚动祖先。  
    粘性定位可以被认为是相对定位和固定定位的混合。元素在跨越特定阈值前为相对定位，之后为固定定位。  

## display

## float

# JavaScript

https://www.bookstack.cn/read/javascript-tutorial/README.md

## 数据类型

```
JavaScript 语言的每一个值，都属于某一种数据类型。JavaScript 的数据类型，共有六种。（ES6 又新增了第七种 Symbol 类型的值，本教程不涉及。）

数值（number）：整数和小数（比如1和3.14）
字符串（string）：文本（比如Hello World）。
布尔值（boolean）：表示真伪的两个特殊值，即true（真）和false（假）
undefined：表示“未定义”或不存在，即由于目前没有定义，所以此处暂时没有任何值
null：表示空值，即此处的值为空。
对象（object）：各种值组成的集合。
通常，数值、字符串、布尔值这三种类型，合称为原始类型（primitive type）的值，即它们是最基本的数据类型，不能再细分了。对象则称为合成类型（complex type）的值，因为一个对象往往是多个原始类型的值的合成，可以看作是一个存放各种值的容器。至于undefined和null，一般将它们看成两个特殊值。

对象是最复杂的数据类型，又可以分成三个子类型。

狭义的对象（object）
数组（array）
函数（function）
狭义的对象和数组是两种不同的数据组合方式，除非特别声明，本教程的“对象”都特指狭义的对象。函数其实是处理数据的方法，JavaScript 把它当成一种数据类型，可以赋值给变量，这为编程带来了很大的灵活性，也为 JavaScript 的“函数式编程”奠定了基础。
```

# TS

## d.ts 文件

类型声明文件