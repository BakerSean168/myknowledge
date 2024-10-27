## Java

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