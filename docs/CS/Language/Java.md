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
String str1 = new String("Hello");
String str2 = new String("Hello");
str1 == str2 // false
str1.equals(str2) // true


### break
break只能跳出与之最近的for，while循环，跟if没有关系。