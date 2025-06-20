# JavaScript

知识来源：  
[阮一峰 js 教程](https://www.bookstack.cn/read/javascript-tutorial/README.md)  
《JavaScript 高级程序设计（第 4 版）》  
https://javascript.info/

## 介绍

起初用于在前端进行数据验证的脚本语言，减少与服务器的通信次数。

包含：

- 核心（ECMAScript）
- 文档对象模型（DOM）  
   提供 HTML、XML 的 API  
   操控表示文档的树
- 浏览器对象模型（BOM）  
   提供 浏览器对象 的 API

## HTML 中的 JavaScript

见 文章

## 语法基础

### 定义变量的三种方式

let
块级作用域  
 变量提升但未初始化  
 需要重新赋值的变量  
const
块级作用域  
 变量提升但未初始化  
 声明常量或引用类型，避免意外修改  
var
函数级作用域  
 提升初始化为 undefined  
 不推荐使用

### 数据类型

原始类型

- 数值（number）：整数和小数（比如 1 和 3.14）
- 字符串（string）：文本（比如 Hello World）。
- 布尔值（boolean）：表示真伪的两个特殊值，即 true（真）和 false（假）
- undefined：表示“未定义”或不存在，变量声明了，但没有赋值
- null：表示空值，即此处的值为空，空对象引用。
- symbol：唯一且不可变的值，用于对象属性的唯一标识。
- bigint：表示任意精度的大整数  
  特点
- 原始类型存储在 stack 中，值直接保存在变量访问的位置
- 复制的是值本身

引用类型

- 狭义的对象（object）
- 数组（array）
- 函数（function）
  特点
- 引用类型存储在 heap 中，变量保存的是实际对象的引用（指针）
- 复制的是引用，多个变量引用同一对象时，一个变量的修改会影响其他变量。

### 操作符

一元操作符、位操作符。。。

### == 和 ===

JavaScript 中的 ==（宽松相等）和 ===（严格相等）是两种不同的比较运算符，核心区别在于 是否进行类型转换 以及 对特殊值的处理规则

## 变量、作用域、内存

### 原始值和引用值

ECMAScript 变量可以包含两种不同类型的数据：原始值和引用值。

- 原始值（primitive value）：  
  就是最简单的数据  
  6 种原始值：Undefined、Null、Boolean、Number、String 和 Symbol。
- 引用值（reference value）：  
  则是由多个值构成的对象。  
  引用值是保存在内存中的对象。

在把一个值赋给变量时，JavaScript 引擎必须确定这个值是原始值还是引用值。
JavaScript 不允许直接访问内存位置，因此也就不能直接操作对象所在的内存空间。

- 保存原始值的变量是**按值（by value）**访问
- 保存引用值的变量是**按引用（by reference）**访问

### 传递参数

ECMAScript 中所有函数的参数都是按值传递的。

### 确定类型

#### typeof

检查变量类型，返回字符串，表示数据类型

```js
console.log(typeof undefined); // "undefined"
console.log(typeof true); // "boolean"
console.log(typeof 42); // "number"
console.log(typeof "hello"); // "string"
console.log(typeof {}); // "object"
console.log(typeof []); // "object"
console.log(typeof null); // "object" (特殊情况)
console.log(typeof function () {}); // "function"
console.log(typeof Symbol()); // "symbol"
console.log(typeof 10n); // "bigint"
```

主要用于基本数据类型、函数、未定义类型、symbol

## 执行上下文与作用域

变量或函数的上下文决定了它们可以访问哪些数据，以及它们的行为。

- 全局执行上下文：全局执行环境是最外围的一个执行环境，在浏览器的全局对象是 window, this 指向这个对象。
- 函数执行上下文：可以有无数个，函数被调用的时候会被创建。每次调用函数都会创建一个新的执行上下文。
- eval 执行上下文，很少用。

每个执行上下文，都有三个重要属性：

- 变量对象 (variable object, VO)  
   每个执行环境都有一个与之关联的变量对象，环境中定义的所有变量和函数都保存在这个对象中。虽然我们编写的代码无法访问这个对象，但解析器在处理数据时会在后台使用它。
- 作用域链（scope chain）  
   当代码在一个环境中执行时，会创建变量对象的一个作用域链。作用域链的用途，是保证对执行环境有权访问的所有变量和函数的有序访问。
- this  
   普通函数指向函数的调用者：有个简便的方法就是看函数前面有没有点，如果有点，那么就指向点前面的那个值;  
   箭头函数指向函数所在的所用域：注意理解作用域，只有函数的{}构成作用域，对象的{}以及 if(){}都不构成作用域;

### 作用域

JavaScript 中的作用域(Scope)是指程序中定义变量的区域，它决定了变量和函数的可访问性和生命周期。

- 全局作用域  
  脚本模式运行所有代码的默认作用域
- 模块作用域  
  模块模式中运行代码的作用域
- 函数作用域  
  由函数创建的作用域
- 块作用域（用 let 或 const 声明的变量属于）  
  解决了 es5 存在的 2 个重要问题
  - 内层变量覆盖外层变量
  - 循环计数变量泄露为全局变量

### 回收机制

垃圾回收（Garbage Collection, GC）  
JavaScript 自动管理内存的核心机制，通过识别和释放不再使用的内存空间，防止内存泄漏并提升性能。  
可达性（Reachability）：从根对象（如全局变量、活动函数的局部变量等）出发，通过引用链无法访问的对象会被视为垃圾。

回收算法

- 标记-清除（Mark-and-Sweep）  
  原理：  
   标记阶段：从根对象出发，递归遍历所有可达对象并标记为活动。  
   清除阶段：遍历堆内存，释放未被标记的对象。  
  优点：  
   能处理循环引用问题  
  缺点：  
   可能产生内存碎片，清除时需要暂停程序。
- 引用计数（Reference Counting）  
  原理：  
   每个对象维护引用计数器，引用数量为 0 时回收。  
  优点：  
   可即时回收内存。  
  缺点：  
   无法解决循环引用问题。

#### 现代 JS 引擎的优化策略

1. 分代收集（Generational Collection）  
   分代假设：大多数对象生命周期短，少数长期存活。  
    新生代：存放短命对象，使用 复制算法（如 V8 的 Scavenge）快速回收。  
    老生代：存放长存对象，采用 标记-清除 + 标记-整理（减少碎片）。
2. 增量标记（Incremental Marking）  
   将标记过程拆分为多个小步骤，穿插在主线程任务中执行，减少程序停顿时间。
3. 闲时收集（Idle-Time Collection）  
   在 CPU 空闲时执行垃圾回收，减少对主线程性能的影响

### 内存管理

将内存占用量保持在一个较小的值可以让页面性能更好。  
优化内存占用的最佳手段就是保证在执行代码时只保存必要的数据。  
如果数据不再必要，那么把它设置为 null，从而释放其引用。这也可以叫作**解除引用**。

1. 使用 const 和 let  
   改进垃圾回收机制
2. 隐藏类和删除操作
3. 内存泄露
4. 静态分配与对象池  
   减少垃圾回收次数

## 基本引用类型

引用值（或者对象）是某个特定引用类型的实例。  
对象被认为是某个特定引用类型的实例。

### Date

### 原始值包装类型

为了方便操作原始值，ECMAScript 提供了 3 种特殊的引用类型：Boolean、Number 和 String。

每当用到某个原始值的方法或属性时，后台都会创建一个相应原始包装类型的对象，从而暴露出操作原始值的各种方法。

Number、Bollean、String

#### String

字符串的原型上暴露了一个@@iterator 方法，表示可以迭代字符串的每个字符。  
有了这个迭代器之后，字符串就可以通过解构操作符来解构了。

```js
let message = "abcde";
console.log([...message]);
```

### 单例内置对象

ECMA-262 对内置对象的定义是“任何由 ECMAScript 实现提供、与宿主环境无关，并在 ECMAScript 程序开始执行时就存在的对象”。  
这就意味着，开发者不用显式地实例化内置对象，因为它们已经实例化好了。  
前面我们已经接触了大部分内置对象，包括 Object、Array 和 String。  
本节介绍 ECMA-262 定义的另外两个单例内置对象：Global 和 Math。

#### Global

为一种兜底对象，它所针对的是不属于任何对象的属性和方法。

- URL 编码方法
- eval（）方法
- Global 对象属性
- window 对象

#### Math

提供了 Math 对象作为保存数学公式、信息和计算的地方。

## 集合引用类型

### Object

创建 Object 实例的方法：

1. new 操作符和 Object 构造函数
2. 对象字面量  
   属性名可以为数字（会自动转换为字符串）或字符串

#### Object 方法

| 方法名                          | 描述                                        | 示例                                                               |
| ------------------------------- | ------------------------------------------- | ------------------------------------------------------------------ |
| `Object.keys(obj)`              | 返回对象自身可枚举属性的键名数组            | `Object.keys({a:1, b:2})` → `["a", "b"]`                           |
| `Object.values(obj)`            | 返回对象自身可枚举属性的键值数组            | `Object.values({a:1, b:2})` → `[1, 2]`                             |
| `Object.entries(obj)`           | 返回对象自身可枚举属性的键值对二维数组      | `Object.entries({a:1, b:2})` → `[["a", 1], ["b", 2]]`              |
| `Object.assign(target, ...src)` | 合并源对象属性到目标对象（浅拷贝）          | `Object.assign({a:1}, {b:2})` → `{a:1, b:2}`                       |
| `Object.create(proto)`          | 创建以指定对象为原型的新对象                | `const obj = Object.create({name: "Alice"}); obj.name` → `"Alice"` |
| `Object.freeze(obj)`            | 冻结对象（不可修改/添加/删除属性）          | `Object.freeze(obj); obj.a = 2` → 修改失败                         |
| `Object.seal(obj)`              | 密封对象（不可添加/删除属性，但可修改值）   | `Object.seal(obj); obj.a = 2` → 修改有效                           |
| `Object.is(val1, val2)`         | 严格值比较（处理 `NaN` 和 `±0`）            | `Object.is(NaN, NaN)` → `true`；`Object.is(0, -0)` → `false`       |
| `Object.fromEntries(entries)`   | 将键值对列表转换为对象                      | `Object.fromEntries([["a",1], ["b",2]])` → `{a:1, b:2}`            |
| `Object.hasOwn(obj, prop)`      | 检查对象自身是否包含指定属性（ES2022 新增） | `Object.hasOwn({a:1}, 'a')` → `true`                               |

### Array

见 文章 JS中的数组

### 定型数组

定型数组（typed array）是 ECMAScript 新增的结构，目的是提升向原生库传输数据的效率。  
实际上，JavaScript 并没有“TypedArray”类型，它所指的其实是一种特殊的包含数值类型的数组。

#### ArrayBuffer

可用于在内存中分配特定数量的字节空间

#### DataView

第一种允许你读写 ArrayBuffer 的视图

ElementType  
字节序  
边界情形

#### 定型数组

定型数组是另一种形式的 ArrayBuffer 视图。虽然概念上与 DataView 接近，但定型数组的区别在于，它特定于一种 ElementType 且遵循系统原生的字节序。相应地，定型数组提供了适用面更广的 API 和更高的性能。  
设计定型数组的目的就是提高与 WebGL 等原生库交换二进制数据的效率。  
由于定型数组的二进制表示对操作系统而言是一种容易使用的格式，JavaScript 引擎可以重度优化算术运算、按位运算和其他对定型数组的常见操作，因此使用它们速度极快。

### Map

与 Object 只能使用数值、字符串或符号作为键不同，Map 可以使用任何 JavaScript 数据类型作为键。

与 Object 类型的一个主要差异是，Map 实例会维护键值对的插入顺序，因此可以根据插入顺序执行迭代操作。

| 比较维度     | Object                                     | Map                                                | 选择建议                    |
| ------------ | ------------------------------------------ | -------------------------------------------------- | --------------------------- |
| **内存占用** | 随键数量线性增加                           | 随键数量线性增加，但相同内存可多存储约 50%的键值对 | 内存敏感场景选择 Map        |
| **插入性能** | 性能较好                                   | 所有浏览器中通常稍快，性能更佳                     | 大量插入操作选择 Map        |
| **查找速度** | 少量键值对时可能更快，支持数组式使用的优化 | 大型数据查找性能相当，不支持特殊优化               | 频繁查找少量数据选择 Object |
| **删除性能** | delete 操作性能较差                        | delete() 操作性能优于插入和查找                    | 频繁删除操作选择 Map        |

#### Map 常用方法

| 操作类型         | 方法/属性          | 语法示例/描述                                                              | 来源参考 |
| ---------------- | ------------------ | -------------------------------------------------------------------------- | -------- |
| **创建 Map**     | `new Map()`        | `const map = new Map();` 或 `new Map([[key1, val1], [key2, val2]])` 初始化 |          |
| **添加键值对**   | `.set(key, value)` | 支持链式调用：`map.set('a', 1).set('b', 2)`                                |          |
| **获取值**       | `.get(key)`        | `map.get('a')` → 返回对应值，不存在返回 `undefined`                        |          |
| **判断键存在**   | `.has(key)`        | `map.has('a')` → 返回布尔值                                                |          |
| **删除键值对**   | `.delete(key)`     | `map.delete('a')` → 成功删除返回 `true`，否则 `false`                      |          |
| **清空 Map**     | `.clear()`         | 删除所有键值对：`map.clear()`                                              |          |
| **获取大小**     | `.size`            | 属性直接访问：`map.size` → 返回键值对数量                                  |          |
| **遍历键**       | `.keys()`          | 返回迭代器：`for (let key of map.keys()) { ... }`                          |          |
| **遍历值**       | `.values()`        | 返回迭代器：`for (let val of map.values()) { ... }`                        |          |
| **遍历键值对**   | `.entries()`       | 返回 `[key, value]` 数组迭代器：`for (let [k,v] of map.entries()) { ... }` |          |
| **迭代全部元素** | `.forEach()`       | `map.forEach((value, key) => { ... })`（注意参数顺序为 `值, 键`）          |          |

### WeakMap

ECMAScript 6 新增的“弱映射”（WeakMap）是一种新的集合类型，为这门语言带来了增强的键/
值对存储机制。WeakMap 是 Map 的“兄弟”类型，其 API 也是 Map 的子集。WeakMap 中的“weak”（弱），
描述的是 JavaScript 垃圾回收程序对待“弱映射”中键的方式。

弱映射中的键只能是 Object 或者继承自 Object 的类型，尝试使用非对象设置键会抛出
TypeError。值的类型没有限制。

### Set

ECMAScript 6 新增的 Set 是一种新集合类型，为这门语言带来集合数据结构。Set 在很多方面都
像是加强的 Map，这是因为它们的大多数 API 和行为都是共有的。

Set 会维护值插入时的顺序，因此支持按顺序迭代。

### WeakSet

ECMAScript 6 新增的“弱集合”（WeakSet）是一种新的集合类型，为这门语言带来了集合数据结
构。WeakSet 是 Set 的“兄弟”类型，其 API 也是 Set 的子集。WeakSet 中的“weak”（弱），描述的
是 JavaScript 垃圾回收程序对待“弱集合”中值的方式。

## 迭代器和生成器

### 迭代器

#### 迭代器模式

迭代器模式（特别是在 ECMAScript 这个语境下）描述了一个方案，即可以把有些结构称为“可迭代对象”（iterable），因为它们实现了正式的 Iterable 接口，而且可以通过迭代器 Iterator 消费。

- 任何实现 Iterable 接口的数据结构都可以被实现 Iterator 接口的结构“消费”（consume）。
- 迭代器（iterator）是按需创建的一次性对象。
- 每个迭代器都会关联一个可迭代对象，而迭代器会暴露迭代其关联可迭代对象的 API。
- 迭代器无须了解与其关联的可迭代对象的结构，只需要知道如何取得连续的值。这种概念上的分离正是 Iterable 和 Iterator 的强大之处。

#### 可迭代协议

实现 Iterable 接口（可迭代协议）要求同时具备两种能力：支持迭代的自我识别能力和创建实现 Iterator 接口的对象的能力。

在 ECMAScript 中，这意味着必须暴露一个属性作为“默认迭代器”，而且这个属性必须使用特殊的 Symbol.iterator 作为键。这个默认迭代器属性必须引用一个迭代器工厂函数，调用这个工厂函数必须返回一个新迭代器。

内置 Iterable 接口的类型：  
字符串、数组、映射、集合、arguments 对象、NodeList 等 DOM 集合类型

实际写代码过程中，不需要显式调用这个工厂函数来生成迭代器。实现可迭代协议的所有类型都会
自动兼容接收可迭代对象的任何语言特性。

#### 迭代器协议

迭代器是一种一次性使用的对象，用于迭代与其关联的可迭代对象。迭代器 API 使用 next()方法
在可迭代对象中遍历数据。每次成功调用 next()，都会返回一个 IteratorResult 对象，其中包含迭
代器返回的下一个值。若不调用 next()，则无法知道迭代器的当前位置。

- 每个迭代器都表示对可迭代对象的一次性有序遍历。不同迭代器的实例相互之间没有联系，只会独
  立地遍历可迭代对象
- 迭代器并不与可迭代对象某个时刻的快照绑定，而仅仅是使用游标来记录遍历可迭代对象的历程。

```js
// 自定义迭代器
class Counter {
  constructor(limit) {
    this.limit = limit;
  }
  [Symbol.iterator]() {
    let count = 1,
      limit = this.limit;
    return {
      next() {
        if (count <= limit) {
          return { done: false, value: count++ };
        } else {
          return { done: true, value: undefined };
        }
      },
    };
  }
}
```

#### 提前终止迭代器

可选的 return()方法用于指定在迭代器提前关闭时执行的逻辑。  
执行迭代的结构在想让迭代器知道它不想遍历到可迭代对象耗尽时，就可以“关闭”迭代器。可能的情况包括：

- for-of 循环通过 break、continue、return 或 throw 提前退出；
- 解构操作并未消费所有值。

return()方法必须返回一个有效的 IteratorResult 对象。简单情况下，可以只返回{ done: true }。

如果迭代器没有关闭，则还可以继续从上次离开的地方继续迭代。

### 生成器

生成器是 ECMAScript 6 新增的一个极为灵活的结构，拥有在一个函数块内暂停和恢复代码执行的能力。  
这种新能力具有深远的影响，比如，使用生成器可以自定义迭代器和实现协程。

#### 生成器基础

生成器的形式是一个函数，函数名称前面加一个星号（\*）表示它是一个生成器。只要是可以定义函数的地方，就可以定义生成器。

```js
// 生成器函数声明
function* generatorFn() {}
// 生成器函数表达式
let generatorFn = function* () {};
// 作为对象字面量方法的生成器函数
let foo = {
  *generatorFn() {},
};
// 作为类实例方法的生成器函数
class Foo {
  *generatorFn() {}
}
// 作为类静态方法的生成器函数
class Bar {
  static *generatorFn() {}
}
```

_箭头函数不能用来定义生成器函数_

#### 通过 yield 中断执行

yield 关键字可以让生成器停止和开始执行，也是生成器最有用的地方。生成器函数在遇到 yield
关键字之前会正常执行。遇到这个关键字后，执行会停止，函数作用域的状态会被保留。停止执行的生
成器函数只能通过在生成器对象上调用 next()方法来恢复执行

1. 生成器对象作为可迭代对象
2. 使用 yield 实现输入和输出
3. 产生可迭代对象  
   可以使用星号增强 yield 的行为，让它能够迭代一个可迭代对象，从而一次产出一个值  
   实际上只是将一个可迭代对象序列化为一连串可以单独产出的值
4. 使用 yield\*实现递归算法

```js
// 生成器作为默认迭代器
class Foo {
  constructor() {
    this.values = [1, 2, 3];
  }
  *[Symbol.iterator]() {
    yield* this.values;
  }
}
const f = new Foo();
for (const x of f) {
  console.log(x);
}
// 1
// 2
// 3
```

#### 提前终止生成器

与迭代器类似，生成器也支持“可关闭”的概念。一个实现 Iterator 接口的对象一定有 next()
方法，还有一个可选的 return()方法用于提前终止迭代器。生成器对象除了有这两个方法，还有第三
个方法：throw()。

与迭代器不同，所有生成器对象都有 return()方法，只要通过它进入关闭状态，就无法恢复了。  
后续调用 next()会显示 done: true 状态，而提供的任何返回值都不会被存储或传播。

## 对象、类、面向对象编程

### 属性类型

ECMA-262 使用一些内部特性来描述属性的特征。这些特性是由为 JavaScript 实现引擎的规范定义
的。因此，开发者不能在 JavaScript 中直接访问这些特性。为了将某个特性标识为内部特性，规范会用
两个中括号把特性的名称括起来，比如[[Enumerable]]。

属性分两种：数据属性和访问器属性。

#### 数据属性

数据属性包含一个保存数据值的位置。  
值会从这个位置读取，也会写入到这个位置。  
数据属性有 4 个特性描述它们的行为。

- [[Configurable]]
- [[Enumerable]]
- [[Writable]]
- [[Value]]

要修改属性的默认特性，就必须使用 Object.defineProperty()方法。

#### 访问器属性

访问器属性不包含数据值。相反，它们包含一个获取（getter）函数和一个设置（setter）函数，不
过这两个函数不是必需的。  
在读取访问器属性时，会调用获取函数，这个函数的责任就是返回一个有效的值。  
在写入访问器属性时，会调用设置函数并传入新值，这个函数必须决定对数据做出什么修改。  
访问器属性有 4 个特性描述它们的行为。

- [[Configurable]]
- [[Enumerable]]
- [[Get]]
- [[Set]]

访问器属性是不能直接定义的，必须使用 Object.defineProperty()。

#### 定义多个属性

Object.defineProperties()

#### 读取属性的特性

用 Object.getOwnPropertyDescriptor()方法可以取得指定属性的属性描述符

### 创建对象

原型、继承、类

#### 工厂模式

```js
function createPerson(name, age, job) {
  let o = new Object();
  o.name = name;
  o.age = age;
  o.job = job;
  o.sayName = function() {
    console.log(this.name);
  };
  return o;
}
let person1 = createPerson("Nicholas", 29, "Software Engineer");
let person2 = createPerson("Greg", 27, "Doctor");
这里，函数createPerson()接收3个参数，根据这几个参数构建了一个包含
```

没有解决对象标识问题（即新创建的对象是什么类型）  
不能用 instanceof 判断对象类型

#### 构造函数模式

```js
function Person(name, age, job) {
  this.name = name;
  this.age = age;
  this.job = job;
  this.sayName = function () {
    console.log(this.name);
  };
}
let person1 = new Person("Nicholas", 29, "Software Engineer");
let person2 = new Person("Greg", 27, "Doctor");
person1.sayName(); // Nicholas
person2.sayName(); // Greg
```

1. 构造函数与普通函数唯一的区别就是调用方式不同。
2. 构造函数的问题  
   定义的方法会重复创建，虽然是相同逻辑  
   可以把函数定义转移到构造函数外部，但全局作用域也因此被搞乱了

#### 原型模式

每个函数都会创建一个 prototype 属性，这个属性是一个对象，包含应该由特定引用类型的实例
共享的属性和方法。实际上，这个对象就是通过调用构造函数创建的对象的原型。使用原型对象的好处
是，在它上面定义的属性和方法可以被对象实例共享。原来在构造函数中直接赋给对象实例的值，可以
直接赋值给它们的原型

```js
function Person() {}
Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function () {
  console.log(this.name);
};
let person1 = new Person();
person1.sayName(); // "Nicholas"
let person2 = new Person();
person2.sayName(); // "Nicholas"
console.log(person1.sayName == person2.sayName); // true
```

1. 理解原型
   无论何时，只要创建一个函数，就会按照特定的规则为这个函数创建一个 prototype 属性（指向
   原型对象）。默认情况下，所有原型对象自动获得一个名为 constructor 的属性，指回与之关联的构
   造函数。对前面的例子而言，Person.prototype.constructor 指向 Person。然后，因构造函数而
   异，可能会给原型对象添加其他属性和方法。
   在自定义构造函数时，原型对象默认只会获得 constructor 属性，其他的所有方法都继承自
   Object。每次调用构造函数创建一个新实例，这个实例的内部[[Prototype]]指针就会被赋值为构
   造函数的原型对象。脚本中没有访问这个[[Prototype]]特性的标准方式，但 Firefox、Safari 和 Chrome
   会在每个对象上暴露**proto**属性，通过这个属性可以访问对象的原型。在其他实现中，这个特性
   完全被隐藏了。关键在于理解这一点：实例与构造函数原型之间有直接的联系，但实例与构造函数之
   间没有。
2. 原型层级  
    在通过对象访问属性时，会按照这个属性的名称开始搜索。搜索开始于对象实例本身。如果在这个
   实例上发现了给定的名称，则返回该名称对应的值。如果没有找到这个属性，则搜索会沿着指针进入原
   型对象，然后在原型对象上找到属性后，再返回对应的值。
3. 原型和 in 操作符
   在单独使用时，in 操作符会在可以通过对象访问指定属性时返回 true，无论该属性是在实例上还是在原型上。
   在 for-in 循环中使用 in 操作符时，可以通过对象访问且可以被枚举的属性都会返回，包括实例属性和原型属性。
4. 属性枚举顺序
   for-in 循环和 Object.keys()的枚举顺序是不确定的，取决于 JavaScript 引擎  
   Object.getOwnPropertyNames()、Object.getOwnPropertySymbols()和 Object.assign()的枚举顺序是确定性的。先以升序枚举数值键，然后以插入顺序枚举字符串和符号键。

原型动态性：  
 因为从原型上搜索值的过程是动态的，所以即使实例在修改原型之前已经存在，任何时候对原型对象所做的修改也会在实例上反映出来。

原型的问题：

1. 弱化了向构造函数传递初始化参数的能力，会导致所有实例默认都取得相同的属性值。
2. 共享特性（引用型数据，会导致修改一个实例的属性，结果全部都修改了

### 继承

继承是面向对象编程中讨论最多的话题。很多面向对象语言都支持两种继承：接口继承和实现继承。前者只继承方法签名，后者继承实际的方法。接口继承在 ECMAScript 中是不可能的，因为函数没有签名。实现继承是 ECMAScript 唯一支持的继承方式，而这主要是通过原型链实现的。

#### 原型链

ECMA-262 把原型链定义为 ECMAScript 的主要继承方式。其基本思想就是通过原型继承多个引用类型的属性和方法。

1. 默认原型  
   所有引用类型都继承自 Object
2. 原型与继承关系  
   原型与实例的关系可以通过两种方式来确定。  
    instanceof、isPrototypeof
3. 关于方法  
   子类有时候需要覆盖父类的方法，或者增加父类没有的方法。为此，这些方法必须在原型赋值之后再添加到原型上。
4. 原型链的问题
   主要问题出现在原型中包含引用值的时候。前面在谈到原型的问题时也提到过，原型中包含的引用值会在所有实例间共享，这也是为什么属性通常会在构造函数中定义而不会定义在原型上的原因。在使用原型实现继承时，原型实际上变成了另一个类型的实例。这意味着原先的实例属性摇身一变成为了原型属性。  
   第二个问题是，子类型在实例化时不能给父类型的构造函数传参。

#### 盗用构造函数

在子类构造函数中调用父类构造函数。  
因为毕竟函数就是在特定上下文中执行代码的简单对象，所以可以使用 apply()和 call()方法以新创建的对象为上下文执行构造函数。

```js
function SuperType() {
  this.colors = ["red", "blue", "green"];
}
function SubType() {
  // 继承SuperType
  SuperType.call(this);
}
let instance1 = new SubType();
instance1.colors.push("black");
console.log(instance1.colors); // "red,blue,green,black"
let instance2 = new SubType();
console.log(instance2.colors); // "red,blue,green"
```

1. 传递参数
   相比于使用原型链，盗用构造函数的一个优点就是可以在子类构造函数中向父类构造函数传参。
2. 盗用构造函数的问题  
   盗用构造函数的主要缺点，也是使用构造函数模式自定义类型的问题：必须在构造函数中定义方法，因此函数不能重用。此外，子类也不能访问父类原型上定义的方法，因此所有类型只能使用构造函数模式。由于存在这些问题，盗用构造函数基本上也不能单独使用。

#### 组合继承

组合继承（有时候也叫伪经典继承）综合了原型链和盗用构造函数，将两者的优点集中了起来。  
基本的思路是使用原型链继承原型上的属性和方法，而通过盗用构造函数继承实例属性。  
这样既可以把方法定义在原型上以实现重用，又可以让每个实例都有自己的属性。

```js
function SuperType(name) {
  this.name = name;
  this.colors = ["red", "blue", "green"];
}
SuperType.prototype.sayName = function () {
  console.log(this.name);
};
function SubType(name, age) {
  // 继承属性
  SuperType.call(this, name);
  this.age = age;
}
// 继承方法
SubType.prototype = new SuperType();
SubType.prototype.sayAge = function () {
  console.log(this.age);
};
let instance1 = new SubType("Nicholas", 29);
instance1.colors.push("black");
console.log(instance1.colors); // "red,blue,green,black"
instance1.sayName(); // "Nicholas";
instance1.sayAge(); // 29
let instance2 = new SubType("Greg", 27);
console.log(instance2.colors); // "red,blue,green"
instance2.sayName(); // "Greg";
instance2.sayAge(); // 27
```

#### 原型式继承

这个 object()函数会创建一个临时构造函数，将传入的对象赋值给这个构造函数的原型，然后返回这个临时类型的一个实例。本质上，object()是对传入的对象执行了一次浅复制。

```js
function object(o) {
  function F() {}
  F.prototype = o;
  return new F();
}
```

#### 寄生式继承

与原型式继承比较接近的一种继承方式是寄生式继承（parasitic inheritance），也是 Crockford 首倡的一种模式。  
寄生式继承背后的思路类似于寄生构造函数和工厂模式：创建一个实现继承的函数，以某种方式增强对象，然后返回这个对象。

```js
function createAnother(original) {
  let clone = object(original); // 通过调用函数创建一个新对象
  clone.sayHi = function () {
    // 以某种方式增强这个对象
    console.log("hi");
  };
  return clone; // 返回这个对象
}
```

#### 寄生式组合继承

JavaScript 高级程序设计 P247

### 类

虽然 ECMAScript 6 类表面上看起来可以支持正式的面向对象编程，但实际上它背后使用的仍然是原型和构造函数的概念。

#### 类定义

```js
// 类声明
class Person {}
// 不会像函数声明一样提升

// 类表达式
const Animal = class {};
// 和函数表达式一样，不能再求值前引用 会等于 undefined
```

- 类可以包含构造函数方法、实例方法、获取函数、设置函数和静态类方法，但这些都不是必需的。空的类定义照样有效。
- 与函数构造函数一样，多数编程风格都建议类名的首字母要大写，以区别于通过它创建的实例。
- 类表达式的名称是可选的。在把类表达式赋值给变量后，可以通过 name 属性取得类表达式的名称字符串。但不能在类表达式作用域外部访问这个标识符。

### 类构造函数

constructor 关键字用于在类定义块内部创建类的构造函数。方法名 constructor 会告诉解释器在使用 new 操作符创建类的新实例时，应该调用这个函数。构造函数的定义不是必需的，不定义构造函数相当于将构造函数定义为空函数。

1. 实例化

```
使用new调用类的构造函数会执行如下操作。
(1) 在内存中创建一个新对象。
(2) 这个新对象内部的[[Prototype]]指针被赋值为构造函数的prototype属性。
(3) 构造函数内部的this被赋值为这个新对象（即this指向新对象）。
(4) 执行构造函数内部的代码（给新对象添加属性）。
(5) 如果构造函数返回非空对象，则返回该对象；否则，返回刚创建的新对象。
```

#### 实例、原型、类成员

类的语法可以非常方便地定义应该存在于实例上的成员、应该存在于原型上的成员，以及应该存在于类本身的成员。

1. 实例成员
   每次通过 new 调用类标识符时，都会执行类构造函数。在这个函数内部，可以为新创建的实例（this）添加“自有”属性。  
   每个实例都对应一个唯一的成员对象，这意味着所有成员都不会在原型上共享。
2. 原型方法与访问器
   为了在实例间共享方法，类定义语法把在类块中定义的方法作为原型方法。  
   类方法等同于对象属性，因此可以使用字符串、符号或计算的值作为键
3. 静态类方法
   可以在类上定义静态方法。这些方法通常用于执行不特定于实例的操作，也不要求存在类的实例。
4. 非函数原型和类成员  
   类定义并不显式支持在原型或类上添加成员数据，但在类定义外部，可以手动添加
5. 迭代器与生成器方法  
   类定义语法支持在原型和类本身上定义生成器方法

#### 继承

虽然类继承使用的是新语法，但背后依旧使用的是原型链。

1. 继承基础  
   ES6 类支持单继承。使用 extends 关键字，就可以继承任何拥有[[Construct]]和原型的对象。很大程度上，这意味着不仅可以继承一个类，也可以继承普通的构造函数
2. 构造函数、HomeObject 和 super()
   派生类的方法可以通过 super 关键字引用它们的原型。这个关键字只能在派生类中使用，而且仅限于类构造函数、实例方法和静态方法内部。在类构造函数中使用 super 可以调用父类构造函数。
3. 抽象基类
   有时候可能需要定义这样一个类，它可供其他类继承，但本身不会被实例化。虽然 ECMAScript 没有专门支持这种类的语法 ，但通过 new.target 也很容易实现。new.target 保存通过 new 关键字调用的类或函数。通过在实例化时检测 new.target 是不是抽象基类，可以阻止对抽象基类的实例化
4. 继承内置类型
   ES6 类为继承内置引用类型提供了顺畅的机制，开发者可以方便地扩展内置类型
5. 类混入

## 代理与反射

### 代理基础

#### 创建空代理

```js
const target = {
  id: 'target'
};
const handler = {};
const proxy = new Proxy(target, handler);
// id 属性会访问同一个值
console.log(target.id);  // target
console.log(proxy.id);   // target
// 给目标属性赋值会反映在两个对象上
// 因为两个对象访问的是同一个值
target.id = 'foo';
console.log(target.id); // foo
console.log(proxy.id);  // foo
// 给代理属性赋值会反映在两个对象上
// 因为这个赋值会转移到目标对象
proxy.id = 'bar';
console.log(target.id); // bar
console.log(proxy.id);  // bar
// hasOwnProperty()方法在两个地方
// 都会应用到目标对象
console.log(target.hasOwnProperty('id')); // true
console.log(proxy.hasOwnProperty('id'));  // true
// Proxy.prototype 是 undefined
// 因此不能使用instanceof 操作符
console.log(target instanceof Proxy); // TypeError: Function has non-object prototype
'undefined' in instanceof check
console.log(proxy instanceof Proxy);  // TypeError: Function has non-object prototype
'undefined' in instanceof check
// 严格相等可以用来区分代理和目标
console.log(target === proxy); // false
```

#### 定义捕获器

使用代理的主要目的是可以定义捕获器（trap）。捕获器就是在处理程序对象中定义的“基本操作的拦截器”。每个处理程序对象可以包含零个或多个捕获器，每个捕获器都对应一种基本操作，可以直接或间接在代理对象上调用。每次在代理对象上调用这些基本操作时，代理可以在这些操作传播到目标对象之前先调用捕获器函数，从而拦截并修改相应的行为。

## 函数

函数实际上是对象。  
每个函数都是 Function 类型的实例，而 Function 也有属性和方法，跟其他引用类型一样。因为函数是对象，所以函数名就是指向函数对象的指针，而且不一定与函数本身紧密绑定。

创建（实例化）函数的方式：

- 声明式
- 函数表达式
- 箭头函数
- new Function

_把函数想象为对象，把函数名想象为指针是很重要的。_

### 箭头函数

箭头函数不能使用 arguments、super 和 new.target，也不能用作构造函数。此外，箭头函数也没有 prototype 属性。  
箭头函数没有自己的 this，它的 this 继承自定义时的外层作用域（词法作用域），且无法通过 call、apply 或 bind 改变。而构造函数需要通过 new 操作符将 this 绑定到新创建的实例对象上。  
箭头函数的定位是轻量级函数表达式，适用于需要固定 this 的场景（如回调函数），而非面向对象的构造函数。ES6 通过限制其构造函数能力，避免误用。

### 函数名

函数名就是指向函数的指针，所以它们跟其他包含对象指针的变量具有相同的行为。这意味着一个函数可以有多个名称。
ECMAScript 6 的所有函数对象都会暴露一个只读的 name 属性，其中包含关于函数的信息。

### 参数

ECMAScript 函数既不关心传入的参数个数，也不关心这些参数的数据类型。

因为 ECMAScript 函数的参数在内部表现为一个数组。函数被调用时总会接收一个数组，但函数并不关心这个数组中包含什么。如果数组中什么也没有，那没问题；如果数组的元素超出了要求，那也没问题。  
事实上，在使用 function 关键字定义（非箭头）函数时，可以在函数内部访问 **arguments 对象**，从中取得传进来的每个参数值。

- arguments 对象可以跟命名参数一起使用
- arguments 对象的值始终会与对应的命名参数同步。
- 为 arguments 对象的长度是根据传入的参数个数，而非定义函数时给出的命名参数个数确定的。

#### 箭头函数的参数

如果函数是使用箭头语法定义的，那么传给函数的参数将不能使用 arguments 关键字访问，而只
能通过定义的命名参数访问。  
但可以在包装函数中把它提供给箭头函数。

### 没有重载

ECMAScript 函数不能像传统编程那样重载。在其他语言比如 Java 中，一个函数可以有两个定义，只要签名（接收参数的类型和数量）不同就行。如前所述，ECMAScript 函数没有签名，因为参数是由包含零个或多个值的数组表示的。没有函数签名，自然也就没有重载。

### 默认参数值

```js
function makeKing(name = "Henry") {
  return `King ${name} VIII`;
}
console.log(makeKing("Louis")); // 'King Louis VIII'
console.log(makeKing()); // 'King Henry VIII'
```

- 在使用默认参数时，arguments 对象的值不反映参数的默认值，只反映传给函数的参数。
- 默认参数值并不限于原始值或对象类型，也可以使用调用函数返回的值

**默认参数作用域与暂时性死区**

- 因为在求值默认参数时可以定义对象，也可以动态调用函数，所以函数参数肯定是在某个作用域中求值的。
- 因为参数是按顺序初始化的，所以后定义默认值的参数可以引用先定义的参数。
- 参数初始化顺序遵循“暂时性死区”规则，即前面定义的参数不能引用后面定义的。

### 参数扩展与收集

#### 扩展参数

console.log(getSum(...values)); // 10

#### 收集参数

```js
function getSum(...values) {
  // 顺序累加values 中的所有值
  // 初始值的总和为0
  return values.reduce((x, y) => x + y, 0);
}
```

收集参数的前面如果还有命名参数，则只会收集其余的参数；如果没有则会得到空数组。因为收集参数的结果可变，所以只能把它作为最后一个参数

```js
// 不可以
function getProduct(...values, lastValue) {}
// 可以
function ignoreFirst(firstValue, ...values) {
  console.log(values);
}
ignoreFirst();       // []
ignoreFirst(1);      // []
ignoreFirst(1,2);    // [2]
ignoreFirst(1,2,3);  // [2, 3]
```

### 函数声明与函数表达式

- 函数声明会在任何代码执行之前先被读取并添加到执行上下文。这个过程叫作函数声明提升（function declaration hoisting）。
- 函数表达式必须等到代码执行到它那一行，才会在执行上下文中生成函数定义。

### 函数作为值

因为函数名在 ECMAScript 中就是变量，所以函数可以用在任何可以使用变量的地方。这意味着不仅可以把函数作为参数传给另一个函数，而且还可以在一个函数中返回另一个函数。

```js
function callSomeFunction(someFunction, someArgument) {
  return someFunction(someArgument);
}
```

函数返回函数

### 函数内部

在 ECMAScript 5 中，函数内部存在两个特殊的对象：arguments 和 this。ECMAScript 6 又新增了 new.target 属性。

#### arguments

- 使用 arguments.callee 就可以让函数逻辑与函数名解耦

#### this

- 在标准函数中，this 引用的是把函数当成方法调用的上下文对象，这时候通常称其为 this 值（在网页的全局上下文中调用函数时，this 指向 windows）。
- 在事件回调或定时回调中调用某个函数时，this 值指向的并非想要的对象。此时将回调函数写成箭头函数就可以解决问题。这是因为箭头函数中的 this 会保留定义该函数时的上下文

```js
function King() {
  this.royaltyName = "Henry";
  // this 引用 King 的实例
  setTimeout(() => console.log(this.royaltyName), 1000);
}

function Queen() {
  this.royaltyName = "Elizabeth";
  // this 引用 window 对象
  setTimeout(function () {
    console.log(this.royaltyName);
  }, 1000);
}
new King(); // Henry
new Queen(); // undefined
```

#### caller

ECMAScript 5 也会给函数对象上添加一个属性：caller。  
这个属性引用的是调用当前函数的函数，或者如果是在全局作用域中调用的则为 null。

#### new.target

ECMAScript 中的函数始终可以作为构造函数实例化一个新对象，也可以作为普通函数被调用。  
ECMAScript 6 新增了检测函数是否使用 new 关键字调用的 new.target 属性。  
如果函数是正常调用的，则 new.target 的值是 undefined；如果是使用 new 关键字调用的，则 new.target 将引用被调用的构造函数。

```js
function King() {
  if (!new.target) {
    throw 'King must be instantiated using "new"';
  }
  console.log('King instantiated using "new"');
}
new King(); // King instantiated using "new"
King(); // Error: King must be instantiated using "new"
```

#### 函数属性和方法

每个函数都有两个属性：length 和 prototype。

- length 属性保存函数定义的命名参数的个数
- prototype 是保存引用类型所有实例方法的地方，这意味着 toString()、valueOf()等方法实际上都保存在 prototype 上，进而由所有实例共享。

函数还有两个方法：apply()和 call()。
这两个方法都会以指定的 this 值来调用函数，即会设置调用函数时函数体内 this 对象的值。

#### 函数表达式

函数表达式看起来就像一个普通的变量定义和赋值，即创建一个函数再把它赋值给一个变量 functionName。这样创建的函数叫作匿名函数（anonymous funtion），因为 function 关键字后面没有标识符。（匿名函数有也时候也被称为兰姆达函数）。未赋值给其他变量的匿名函数的 name 属性是空字符串。

### 递归

### 尾调用优化

ECMAScript 6 规范新增了一项内存管理优化机制，让 JavaScript 引擎在满足条件时可以重用栈帧。  
具体来说，这项优化非常适合“尾调用”，即外部函数的返回值是一个内部函数的返回值。

### 闭包

- 闭包是指有权访问另一个函数作用域中变量的函数。
- 闭包通常用来创建内部变量，使得 这些变量不能被外部随意修改，同时又可以通过指定的接口来操作。
- 由于闭包会保持对外部作用域的引用，所以它的内存不会被自动回收，容易导致内存泄漏。

优点：

- 保护变量
- 延长变量生命周期
- 实现模块化
- 保持状态

缺点：

- 内存占用
- 性能损耗  
  涉及作用域链查找过程，会带来一定性能损耗。

特性：

- 函数嵌套  
  闭包的实现依赖于函数嵌套，即在一个函数内部定义另一个函数。
- 记忆外部变量
- 延长作用域链
- 返回函数

#### 应用

- 自执行函数
- 防抖
- 节流
- 函数柯里化  
  函数柯里化（Currying）是一种将多个参数的函数转换为一系列接受单个参数的函数的过程。
- 链式调用
- 迭代器
- 发布-订阅模式

#### 问题

闭包造成的内存泄漏怎么解决？  
 闭包中的内存泄漏指的是在闭包函数中，由于对外部变量的引用而导致这些变量无法被垃圾回收机制释放的情况。当一个函数内部定义了一个闭包，并且这个闭包引用了外部变量时，如果这个闭包被其他地方持有，就会导致外部变量无法被正常释放，从而造成内存泄漏。  
 解决闭包中的内存泄漏问题通常需要注意解除外部变量和闭包函数的引用，以及解绑函数本身的引用，使得闭包中引用的外部变量和闭包函数能够被垃圾回收机制释放。

```js

function createClosure() {
  let value = 'Hello';
​
  // 闭包函数
  var closure = function() {
    console.log(value);
  };
​
  // 解绑定闭包函数，并释放资源
  var releaseClosure = function() {
    value = null; // 解除外部变量的引用
    closure = null; // 解除闭包函数的引用
    releaseClosure = null; // 解除解绑函数的引用
  };
​
  // 返回闭包函数和解绑函数
  return {
    closure,
    releaseClosure
  };
}
​
// 创建闭包
var closureObj = createClosure();
​
// 调用闭包函数
closureObj.closure(); // 输出：Hello
​
// 解绑闭包并释放资源
closureObj.releaseClosure();
​
// 尝试调用闭包函数，此时已解绑，不再引用外部变量
closureObj.closure(); // 输出：null

```

#### 防抖

防抖的核心是 延迟执行：高频事件触发后，若在指定时间间隔内再次触发，则重置计时器；只有最后一次触发后的等待时间结束，才会执行目标函数。

```js
// 基础版本
function debounce(func, delay) {
  let timer;
  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => {
      func.apply(this, args);
    }, delay);
  };
}

//支持立即执行版本
function debounce(func, delay, immediate = false) {
  let timer;
  return function (...args) {
    const callNow = immediate && !timer;
    clearTimeout(timer);
    timer = setTimeout(() => {
      if (!immediate) func.apply(this, args);
      timer = null;
    }, delay);
    if (callNow) func.apply(this, args);
  };
}
```

应用场景：

- 搜索框输入联想（用户停止输入后发送请求）
- 窗口大小调整后重新布局
- 表单验证（停止输入后统一校验）

#### 节流

节流的本质是 频率限制：无论事件触发多频繁，在固定时间间隔内最多执行一次目标函数。

```js
// 时间戳版（立即执行）
function throttle(func, limit) {
  let last = 0;
  return function (...args) {
    const now = Date.now();
    if (now - last >= limit) {
      func.apply(this, args);
      last = now;
    }
  };
}

// 定时器版（延迟执行）
function throttle(func, limit) {
  let timer;
  return function (...args) {
    if (!timer) {
      timer = setTimeout(() => {
        func.apply(this, args);
        timer = null;
      }, limit);
    }
  };
}

// 优化版本（结合首次和最后一次执行）
function throttle(func, limit, { leading = true, trailing = true }) {
  let last = 0,
    timer;
  return function (...args) {
    const now = Date.now();
    if (leading && now - last >= limit) {
      func.apply(this, args);
      last = now;
    } else if (trailing && !timer) {
      timer = setTimeout(() => {
        if (trailing) func.apply(this, args);
        timer = null;
        last = now;
      }, limit - (now - last));
    }
  };
}
```

### 立即调用的函数表达式

立即调用的匿名函数又被称作立即调用的函数表达式（IIFE，Immediately Invoked Function Expression）。  
它类似于函数声明，但由于被包含在括号中，所以会被解释为函数表达式。紧跟在第一组括号后面的第二组括号会立即调用前面的函数表达式。

### 私有变量

严格来讲，JavaScript 没有私有成员的概念，所有对象属性都公有的。不过，倒是有私有变量的概念。任何定义在函数或块中的变量，都可以认为是私有的，因为在这个函数或块的外部无法访问其中的变量。私有变量包括函数参数、局部变量，以及函数内部定义的其他函数。

1. 静态私有变量
   特权方法也可以通过使用私有作用域定义私有变量和函数来实现。
2. 模块模式
   在一个单例对象上实现了相同的隔离和封装。单例对象（singleton）就是只有一个实例的对象。
3. 模块增强模式  
   在返回对象之前先对其进行增强。这适合单例对象需要是某个特定类型的实例，但又必须给它添加额外属性或方法的场景。

## 期约与异步函数

### 异步编程

#### 同步与异步

#### 以往的异步编程模式

### 期约

期约是对尚不存在结果的一个替身。

#### Promises/A+规范

早期的期约机制在 jQuery 和 Dojo 中是以 Deferred API 的形式出现的。到了 2010 年，CommonJS 项目实现的 Promises/A 规范日益流行起来。  
ECMAScript 6 增加了对 Promises/A+规范的完善支持，即 Promise 类型。一经推出，Promise 就大受欢迎，成为了主导性的异步编程机制。

#### 期约基础

ECMAScript 6 新增的引用类型 Promise，可以通过 new 操作符来实例化。创建新期约时需要传入执行器（executor）函数作为参数

1. 期约状态机  
   待定（pending）  
   兑现（fulfilled，或者 resolved）  
   拒绝（rejected）  
   待定（pending）是期约的最初始状态。在待定状态下，期约可以落定（settled）为代表成功的兑现（fulfilled）状态，或者代表失败的拒绝（rejected）状态。无论落定为哪种状态都是不可逆的。只要从待定转换为兑现或拒绝，期约的状态就不再改变。而且，也不能保证期约必然会脱离待定状态。因此，组织合理的代码无论期约解决（resolve）还是拒绝（reject），甚至永远处于待定（pending）状态，都应该具有恰当的行为。
2. 解决值、拒绝理由及期约用例
3. 通过执行函数控制期约状态
4. Promise.resolve()
5. Promise.reject()
6. 同步/异步执行的二元性

## BOM

见 文章 JS中的BOM

## 客户端检测

能力检测，在使用之前先测试浏览器的特定能力。  
用户代理检测，通过用户代理字符串确定浏览器。

## DOM

文档对象模型（DOM，Document Object Model）是 HTML 和 XML 文档的编程接口。  
DOM 表示由多层节点构成的文档，通过它开发者可以添加、删除和修改页面的各个部分。

Document Object Model, 文档对象模型

- 元素（element）  
  文档中的所有标签都是元素，元素可以看成是对象
- 节点（node）  
  文档中所有的内容都是节点：标签，属性，文本
- 文档（document）  
  一个页面就是一个文档

文档包含节点，节点包含元素

### 节点层级

任何 HTML 或 XML 文档都可以用 DOM 表示为一个由节点构成的层级结构。  
节点分很多类型，每种类型对应着文档中不同的信息和（或）标记，也都有自己不同的特性、数据和方法，而且与其他类型有某种关系。  
这些关系构成了层级，让标记可以表示为一个以特定节点为根的树形结构。

#### Node 类型

DOM Level 1 描述了名为 Node 的接口，这个接口是所有 DOM 节点类型都必须实现的。  
Node 接口在 JavaScript 中被实现为 Node 类型，在除 IE 之外的所有浏览器中都可以直接访问这个类型。  
在 JavaScript 中，所有节点类型都继承 Node 类型，因此所有类型都共享相同的基本属性和方法。

每个节点都有 nodeType 属性，表示该节点的类型。  
节点类型由定义在 Node 类型上的 12 个数值常量表示

1. nodeName 与 nodeValue
   nodeName 与 nodeValue 保存着有关节点的信息。这两个属性的值完全取决于节点类型。
2. 节点关系  
   文档中的所有节点都与其他节点有关系。
3. 操纵节点
4. 其他方法  
   cloneNode()  
    会返回与调用它的节点一模一样的节点。  
    normalize()  
    处理文档子树中的文本节点。

```js
// 取：
document.getElementById();

// 获取节点所有属性
node.attributes;

// 获取节点所有子元素
node.childNodes;

// 增：
let a = createElement("a");
document.body.append(a);

// 删：
document.body.removeChild(div);
```

#### Document 类型

Document 类型是 JavaScript 中表示文档节点的类型。  
在浏览器中，文档对象 document 是 HTMLDocument 的实例（HTMLDocument 继承 Document），表示整个 HTML 页面。  
document 是 window 对象的属性，因此是一个全局对象。

1. 文档子节点  
   虽然 DOM 规范规定 Document 节点的子节点可以是 DocumentType、Element、Processing- Instruction 或 Comment，但也提供了两个访问子节点的快捷方式。  
   documentElement 属性，始终指向 HTML 页面中的`<html>`元素。  
   document.body 属性，指向`<body>`
2. 文档信息
   title、URL、domain、referrer
3. 定位元素
4. 特殊集合
   document 对象上还暴露了几个特殊集合，这些集合也都是 HTMLCollection 的实例。  
   这些集合是访问文档中公共部分的快捷方式。  
    document.anchors 包含文档中所有带 name 属性的`<a>`元素。
5. DOM 兼容性检测
   由于 DOM 有多个 Level 和多个部分，因此确定浏览器实现了 DOM 的哪些部分是很必要的。
6. 文档写入
   document 对象有一个古老的能力，即向网页输出流中写入内容。  
   这个能力对应 4 个方法：write()、writeln()、open()和 close()。

#### Element 类型

Element 表示 XML 或 HTML 元素，对外暴露出访问元素标签名、子节点和属性的能力。

- nodeType = 1
- nodeName 值为元素的标签名
- nodeValue = null
- parentNode = Document || Element
- 子节点可以是 Element、Text、Comment、ProcessingInstruction、CDATASection、EntityReference 类型。

可以通过 nodeName 或 tagName 属性来获取元素的标签名。

#### Text 类型

Text 节点由 Text 类型表示，包含按字面解释的纯文本，也可能包含转义后的 HTML 字符，但不含 HTML 代码。

- nodeType = 3
- nodeName = "#text"
- nodeValue = 节点中包含的文本
- parentNode = Element 对象
- 不支持子节点

默认情况下，包含文本内容的每个元素最多只能有一个文本节点。  
只要开始标签和结束标签之间有内容，就会创建一个文本节点

#### Comment 类型

DOM 中的注释通过 Comment 类型表示。

- nodeType = 8
- nodeName= "#comment"
- nodeValue = 注释的内容
- parentNode = Document 或 Element 对象
- 不支持子节点

Comment 类型与 Text 类型继承同一个基类（CharacterData），因此拥有除 splitText()之外 Text 节点所有的字符串操作方法。  
与 Text 类型相似，注释的实际内容可以通过 nodeValue 或 data 属性获得。

#### CDATASection 类型

CDATASection 类型表示 XML 中特有的 CDATA 区块。  
CDATASection 类型继承 Text 类型，因此拥有包括 splitText()在内的所有字符串操作方法。

#### DocumentType 类型

DocumentType 类型的节点包含文档的文档类型（doctype）信息

#### DocumentFragment 类型

在所有节点类型中，DocumentFragment 类型是唯一一个在标记中没有对应表示的类型。  
DOM 将文档片段定义为“轻量级”文档，能够包含和操作节点，却没有完整文档那样额外的消耗。

#### Attr 类型

元素数据在 DOM 中通过 Attr 类型表示。  
Attr 类型构造函数和原型在所有浏览器中都可以直接访问。  
技术上讲，属性是存在于元素 attributes 属性中的节点。

##### 改变节点中的文本值

##### innerHTML、innerText、textContent

- innerHTML  
  表示所有 HTML  
  Element 对象的属性
- innerText  
  表示所有文本内容  
  HTMLElement 对象的属性
- textContent  
  返回的是字符串或 null  
  修改该属性会删除其他全部节点  
  Node 对象的属性

innerText 会触发回流，但是 textContent 可能不会触发回流，所以实际应用中，使用 textContent 性能更佳  
innerTTML 会返回 HTML 文本，textContent 的内容不会解析成 HTML 文本，使用 textContent 可以防止 XSS 攻击

### DOM 编程

动态脚本  
动态样式  
操作表格  
使用 NodeList

### MutationObserver 接口

可以在 DOM 被修改时异步执行回调。  
使用 MutationObserver 可以观察整个文档、DOM 树的一部分，或某个元素。  
此外还可以观察元素属性、子节点、文本，或者前三者任意组合的变化。

## DOM 扩展

### Selectors API

Selectors API Level 1 的核心是两个方法：querySelector()和 querySelectorAll()。  
在兼容浏览器中，Document 类型和 Element 类型的实例上都会暴露这两个方法。

### 元素遍历

### HTML5

#### CSS 类扩展

1. getElementsByClassName()
2. classList 属性

#### 焦点管理

document.activeElement，始终包含当前拥有焦点的 DOM 元素。  
document.hasFocus()方法，该方法返回布尔值，表示文档是否拥有焦点。

#### HTMLDocument 扩展

1. readyState 属性
   loading，表示文档正在加载  
   complete，表示文档加载完成
2. compatMode 属性  
   指示浏览器当前处于什么渲染模式
3. head 属性
   document.head 指向 head

#### 字符集属性

#### 自定义数据属性

#### 插入标记

#### scrollIntoView()

scrollIntoView()方法存在于所有 HTML 元素上，可以滚动浏览器窗口或容器元素以便包含元素进入视口。

这个方法可以用来在页面上发生某个事件时引起用户关注。  
把焦点设置到一个元素上也会导致浏览器将元素滚动到可见位置。

## DOM2 到 DOM3

DOM1（DOM Level 1）主要定义了 HTML 和 XML 文档的底层结构。  
DOM2（DOM Level 2）和 DOM3（DOM Level 3）在这些结构之上加入更多交互能力，提供了更高级的 XML 特性。  
实际上，DOM2 和 DOM3 是按照模块化的思路来制定标准的，每个模块之间有一定关联，但分别针对某个 DOM 子集。

```
 DOM Core：在DOM1核心部分的基础上，为节点增加方法和属性。
 DOM Views：定义基于样式信息的不同视图。
 DOM Events：定义通过事件实现DOM文档交互。
 DOM Style：定义以编程方式访问和修改CSS样式的接口。
 DOM Traversal and Range：新增遍历 DOM文档及选择文档内容的接口。
 DOM HTML：在DOM1 HTML部分的基础上，增加属性、方法和新接口。
 DOM Mutation Observers：定义基于 DOM变化触发回调的接口。这个模块是DOM4级模块，
用于取代Mutation Events。
```

## 事件

JavaScript 与 HTML 的交互是通过事件实现的，事件代表文档或浏览器窗口中某个有意义的时刻。  
可以使用仅在事件发生时执行的监听器（也叫处理程序）订阅事件。  
在传统软件工程领域，这个模型叫“观察者模式”，其能够做到页面行为（在 JavaScript 中定义）与页面展示（在 HTML 和 CSS 中定义）的分离。

### 事件流

事件流描述了页面接收事件的顺序。

#### 事件冒泡

IE 事件流被称为事件冒泡，这是因为事件被定义为从最具体的元素（文档树中最深的节点）开始触发，然后向上传播至没有那么具体的元素（文档）。

#### 事件捕获

事件捕获的意思是最不具体的节点应该最先收到事件，而最具体的节点应该最后收到事件。  
事件捕获实际上是为了在事件到达最终目标前拦截事件。

#### DOM 事件流

DOM2 Events 规范规定事件流分为 3 个阶段：事件捕获、到达目标和事件冒泡。  
事件捕获最先发生，为提前拦截事件提供了可能。  
然后，实际的目标元素接收到事件。最后一个阶段是冒泡，最迟要在这个阶段响应事件。

### 事件处理程序

事件意味着用户或浏览器执行的某种动作。  
比如，单击（click）、加载（load）、鼠标悬停（mouseover）。  
为响应事件而调用的函数被称为事件处理程序（或事件监听器）。  
事件处理程序的名字以"on"开头，因此 click 事件的处理程序叫作 onclick，而 load 事件的处理程序叫作 onload。

#### HTML 事件处理程序

特定元素支持的每个事件都可以使用事件处理程序的名字以 HTML 属性的形式来指定。

### 事件对象

在 DOM 中发生事件时，所有相关信息都会被收集并存储在一个名为**event**的对象中。  
这个对象包含了一些基本信息，比如导致事件的元素、发生的事件类型，以及可能与特定事件相关的任何其他数据。  
例如，鼠标操作导致的事件会生成鼠标位置信息，而键盘操作导致的事件会生成与被按下的键有关的信息。

### 事件类型

Web 浏览器中可以发生很多种事件。  
如前所述，所发生事件的类型决定了事件对象中会保存什么信息。

```
DOM3 Events定义了如下事件类型。
 用户界面事件（UIEvent）：涉及与BOM交互的通用浏览器事件。
 焦点事件（FocusEvent）：在元素获得和失去焦点时触发。
 鼠标事件（MouseEvent）：使用鼠标在页面上执行某些操作时触发。
 滚轮事件（WheelEvent）：使用鼠标滚轮（或类似设备）时触发。
 输入事件（InputEvent）：向文档中输入文本时触发。
 键盘事件（KeyboardEvent）：使用键盘在页面上执行某些操作时触发。
 合成事件（CompositionEvent）：在使用某种IME（Input Method Editor，输入法编辑器）输入
字符时触发。
```

#### 用户界面事件

1. load 事件
   在 window 对象上，load 事件会在整个页面（包括所有外部资源如图片、JavaScript 文件和 CSS 文件）加载完成后触发。
2. unload 事件
   在文档卸载完成后触发。unload 事件一般是在从一个页面导航到另一个页面时触发，最常用于清理引用，以避免内存泄漏。
3. resize 事件
4. scroll 事件

#### 焦点事件

焦点事件在页面元素获得或失去焦点时触发。  
这些事件可以与 document.hasFocus()和 document.activeElement 一起为开发者提供用户在页面中导航的信息。

当焦点从页面中的一个元素移到另一个元素上时，会依次发生如下事件。
(1) focuscout 在失去焦点的元素上触发。
(2) focusin 在获得焦点的元素上触发。
(3) blur 在失去焦点的元素上触发。
(4) DOMFocusOut 在失去焦点的元素上触发。
(5) focus 在获得焦点的元素上触发。
(6) DOMFocusIn 在获得焦点的元素上触发。
其中，blur、DOMFocusOut 和 focusout 的事件目标是失去焦点的元素，而 focus、DOMFocusIn
和 focusin 的事件目标是获得焦点的元素。

#### 鼠标和滚轮事件

 click：在用户单击鼠标主键（通常是左键）或按键盘回车键时触发。这主要是基于无障碍的考
虑，让键盘和鼠标都可以触发 onclick 事件处理程序。
 dblclick：在用户双击鼠标主键（通常是左键）时触发。这个事件不是在 DOM2 Events 中定义
的，但得到了很好的支持，DOM3 Events 将其进行了标准化。
 mousedown：在用户按下任意鼠标键时触发。这个事件不能通过键盘触发。
 mouseenter：在用户把鼠标光标从元素外部移到元素内部时触发。这个事件不冒泡，也不会在
光标经过后代元素时触发。mouseenter 事件不是在 DOM2 Events 中定义的，而是 DOM3 Events
中新增的事件。
 mouseleave：在用户把鼠标光标从元素内部移到元素外部时触发。这个事件不冒泡，也不会在
光标经过后代元素时触发。mouseleave 事件不是在 DOM2 Events 中定义的，而是 DOM3 Events
中新增的事件。
 mousemove：在鼠标光标在元素上移动时反复触发。这个事件不能通过键盘触发。
 mouseout：在用户把鼠标光标从一个元素移到另一个元素上时触发。移到的元素可以是原始元
素的外部元素，也可以是原始元素的子元素。这个事件不能通过键盘触发。
 mouseover：在用户把鼠标光标从元素外部移到元素内部时触发。这个事件不能通过键盘触发。
 mouseup：在用户释放鼠标键时触发。这个事件不能通过键盘触发。

页面中的所有元素都支持鼠标事件。除了 mouseenter 和 mouseleave，所有鼠标事件都会冒泡，都可以被取消，而这会影响浏览器的默认行为。

比如，click 事件触发的前提是 mousedown 事件触发后，紧接着又在同一个元素上触发了 mouseup 事件。如果 mousedown 和 mouseup 中的任意一个事件被取消，那么 click 事件就不会触发。

#### 键盘与输入事件

键盘事件包含 3 个事件：
 keydown，用户按下键盘上某个键时触发，而且持续按住会重复触发。
 keypress，用户按下键盘上某个键并产生字符时触发，而且持续按住会重复触发。Esc 键也会
触发这个事件。DOM3 Events 废弃了 keypress 事件，而推荐 textInput 事件。
 keyup，用户释放键盘上某个键时触发。

当用户按下键盘上的某个字符键时，首先会触发 keydown 事件，然后触发 keypress 事件，最后触发 keyup 事件。  
注意，这里 keydown 和 keypress 事件会在文本框出现变化之前触发，而 keyup 事件会在文本框出现变化之后触发。  
如果一个字符键被按住不放，keydown 和 keypress 就会重复触发，直到这个键被释放。

对于非字符键，在键盘上按一下这个键，会先触发 keydown 事件，然后触发 keyup 事件。  
如果按住某个非字符键不放，则会重复触发 keydown 事件，直到这个键被释放，此时会触发 keyup 事件。

**textInput 事件**

- 对 keypress 的替代
- 只在可编辑区域上触发。
- 只在有新字符被插入时才会触发

#### 合成事件

合成事件是 DOM3 Events 中新增的，用于处理通常使用 IME 输入时的复杂输入序列。  
IME 可以让用户输入物理键盘上没有的字符。

#### HTML5 事件

1. contextmenu 事件
2. beforeunload 事件
   给开发者提供阻止页面被卸载的机会

### 内存与性能

在 JavaScript 中，页面中事件处理程序的数量与页面整体性能直接相关。原因有很多。首先，每个函数都是对象，都占用内存空间，对象越多，性能越差。其次，为指定事件处理程序所需访问 DOM 的次数会先期造成整个页面交互的延迟。只要在使用事件处理程序时多注意一些方法，就可以改善页面性能。

#### 事件委托

“过多事件处理程序”的解决方案是使用事件委托。  
事件委托利用事件冒泡，可以只使用一个事件处理程序来管理一种类型的事件。

#### 删除事件处理程序

### 模拟事件

以通过 JavaScript 在任何时候触发任意事件

## 动画与 Canvas 图形

## 客户端存储

- Cookie  
  约 4KB（每个域名）  
  可设置过期时间，默认会话结束时失效。
- Web Storage
  localStorage  
   5-10MB  
   永久存储，需要手动清除  
  sessionStorage  
   页面会话结束时清除
- IndexedDB  
   支持异步操作  
   适用于离线应用
- Cache API  
   与 Service Worker 配合，缓存网络请求资源，支持 PWA 离线访问  
   存储请求-响应对，常用于静态资源（HTML/CSS/JS）的离线缓存
- 内存缓存  
   全局变量或状态管理工具（如 Vuex、Redux）  
   数据仅在页面刷新前有效，响应速度快，适合高频访问的临时状态（如用户登录信息）。

### cookie

用于在客户端存储会话信息

求服务器在响应 HTTP 请求时，通过发送 Set-Cookie HTTP 头部包含会话信息。  
浏览器会存储这些会话信息，并在之后的每个请求中都会通过 HTTP 头部 cookie 再将它们发回服务器。

#### 限制

cookie 是与特定域绑定的。设置 cookie 后，它会与请求一起发送到创建它的域。  
这个限制能保证 cookie 中存储的信息只对被认可的接收者开放，不被其他域访问。

#### cookie 的构成

cookie 在浏览器中是由以下参数构成的。

```
 名称：唯一标识cookie的名称。cookie名不区分大小写，因此myCookie 和MyCookie 是同一
个名称。不过，实践中最好将 cookie 名当成区分大小写来对待，因为一些服务器软件可能这样
对待它们。cookie名必须经过URL编码。
 值：存储在cookie里的字符串值。这个值必须经过URL编码。
 域：cookie有效的域。发送到这个域的所有请求都会包含对应的cookie。这个值可能包含子域（如
www.wrox.com），也可以不包含（如.wrox.com表示对 wrox.com的所有子域都有效）。如果不明
确设置，则默认为设置cookie的域。
 路径：请求URL中包含这个路径才会把 cookie发送到服务器。例如，可以指定 cookie只能由
http://www.wrox.com/books/访问，因此访问 http://www.wrox.com/下的页面就不会发送 cookie，即
使请求的是同一个域。
 过期时间：表示何时删除cookie的时间戳（即什么时间之后就不发送到服务器了）。默认情况下，
浏览器会话结束后会删除所有cookie。不过，也可以设置删除cookie的时间。这个值是GMT格
式（Wdy, DD-Mon-YYYY HH:MM:SS GMT），用于指定删除cookie的具体时间。这样即使关闭
浏览器cookie也会保留在用户机器上。把过期时间设置为过去的时间会立即删除cookie。
 安全标志：设置之后，只在使用SSL安全连接的情况下才会把cookie发送到服务器。例如，请
求https://www.wrox.com会发送 cookie，而请求 http://www.wrox.com则不会。

HTTP/1.1 200 OK
Content-type: text/html
Set-Cookie: name=value; expires=Mon, 22-Jan-07 07:10:24 GMT; domain=.wrox.com
Other-header: other-header-value
这个头部设置一个名为"name"的 cookie，这个 cookie 在 2007 年 1 月 22 日 7:10:24 过期，对
www.wrox.com及其他wrox.com的子域（如p2p.wrox.com）有效。
安全标志secure是cookie中唯一的非名/值对，只需一个secure就可以了。比如：
HTTP/1.1 200 OK
Content-type: text/html
Set-Cookie: name=value; domain=.wrox.com; path=/; secure
Other-header: other-header-value
```

#### 子 cookie

是使用 cookie 的值在单个 cookie 中存储多个名/值对

#### 使用 cookie 的注意事项

有一种叫作 HTTP-only 的 cookie。  
HTTP-only 可以在浏览器设置，也可以在服务器设置，但只能在服务器上读取，这是因为 JavaScript 无法取得这种 cookie 的值。  
因为所有 cookie 都会作为请求头部由浏览器发送给服务器，所以在 cookie 中保存大量信息可能会影响特定域浏览器请求的性能。  
保存的 cookie 越大，请求完成的时间就越长。  
即使浏览器对 cookie 大小有限制，最好还是尽可能只通过 cookie 保存必要信息，以避免性能问题。

### Web Storage

#### Storage 类型

Storage 类型用于保存名/值对数据，直至存储空间上限（由浏览器决定）

#### sessionStorage 对象

sessionStorage 对象只存储会话数据，这意味着数据只会存储到浏览器关闭。  
这跟浏览器关闭时会消失的会话 cookie 类似。存储在 sessionStorage 中的数据不受页面刷新影响，可以在浏览器崩溃并重启后恢复。

#### localStorage

作为在客户端持久存储数据的机制。  
要访问同一个 localStorage 对象，页面必须来自同一个域（子域不可以）、在相同的端口上使用相同的协议。

存储在 localStorage 中的数据会保留到通过 JavaScript 删除或者用户清除浏览器缓存。  
localStorage 数据不受页面刷新影响，也不会因关闭窗口、标签页或重新启动浏览器而丢失。

#### 存储事件

每当 Storage 对象发生变化时，都会在文档上触发 storage 事件。

### IndexedDB

## 模块模式

### 理解模块模式

把逻辑分块，各自封装，相互独立，每个块自行决定对外暴露什么，同时自行决定引入执行哪些外部代码。

#### 模块标识符

模块标识符是所有模块系统通用的概念。  
模块系统本质上是键/值实体，其中每个模块都有个可用于引用它的标识符。  
这个标识符在模拟模块的系统中可能是字符串，在原生实现的模块系统中可能是模块文件的实际路径。

#### 模块依赖

模块系统的核心是管理依赖。  
指定依赖的模块与周围的环境会达成一种契约。  
本地模块向模块系统声明一组外部模块（依赖），这些外部模块对于当前模块正常运行是必需的。  
模块系统检视这些依赖，进而保证这些外部模块能够被加载并在本地模块运行时初始化所有依赖。

#### 模块加载

在浏览器中，加载模块涉及几个步骤。

- 加载模块涉及执行其中的代码，但必须是在所有依赖都加载并执行之后。
- 如果浏览器没有收到依赖模块的代码，则必须发送请求并等待网络返回。
- 收到模块代码之后，浏览器必须确定刚收到的模块是否也有依赖。
- 然后递归地评估并加载所有依赖，直到所有依赖模块都加载完成。
- 只有整个依赖图都加载完成，才可以执行入口模块。

#### 入口

相互依赖的模块必须指定一个模块作为入口（entry point），这也是代码执行的起点。

#### 异步依赖

可以让 JavaScript 通知模块系统在必要时加载新模块，并在模块加载完成后提供回调。

#### 动态依赖

允许开发者在程序结构中动态添加依赖。

#### 静态分析

模块中包含的发送到浏览器的 JavaScript 代码经常会被静态分析，分析工具会检查代码结构并在不实际执行代码的情况下推断其行为。  
对静态分析友好的模块系统可以让模块打包系统更容易将代码处理为较少的文件。

#### 循环依赖

要构建一个没有循环依赖的 JavaScript 应用程序几乎是不可能的，因此包括 CommonJS、AMD 和 ES6 在内的所有模块系统都支持循环依赖。

### 凑合的模块系统

为按照模块模式提供必要的封装，ES6 之前的模块有时候会使用函数作用域和立即调用函数表达式（IIFE，Immediately Invoked Function Expression）将模块定义封装在匿名闭包中。

### 使用 ES6 之前的模块加载器

#### CommonJS

CommonJS 规范概述了同步声明依赖的模块定义。  
这个规范主要用于在服务器端实现模块化代码组织，但也可用于定义在浏览器中使用的模块依赖。  
CommonJS 模块语法不能在浏览器中直接运行。

无论一个模块在 require()中被引用多少次，模块永远是单例。

#### 异步模块定义

CommonJS 以服务器端为目标环境，能够一次性把所有模块都加载到内存  
而异步模块定义（AMD，Asynchronous Module Definition）的模块定义系统则以浏览器为目标执行环境

AMD 模块实现的核心是用函数包装模块定义。

#### 通用模块定义

为了统一 CommonJS 和 AMD 生态系统，通用模块定义（UMD，Universal Module Definition）规范
应运而生。  
UMD 可用于创建这两个系统都可以使用的模块代码。  
本质上，UMD 定义的模块会在启动时检测要使用哪个模块系统，然后进行适当配置，并把所有逻辑包装在一个立即调用的函数表达式（IIFE）中。

### 使用 ES6 模块

ES6 最大的一个改进就是引入了模块规范。这个规范全方位简化了之前出现的模块加载器，原生浏
览器支持意味着加载器及其他预处理都不再必要。从很多方面看，ES6 模块系统是集 AMD 和 CommonJS
之大成者。

#### 模块标签及定义

ECMAScript 6 模块是作为一整块 JavaScript 代码而存在的。  
带有 type="module"属性的`<script>`标签会告诉浏览器相关代码应该作为模块执行，而不是作为传统的脚本执行。

- 所有模块都会像`<script defer>`加载的脚本一样按顺序执行。
  解析到`<script type="module">`标签后会立即下载模块文件，但执行会延迟到文档解析完成。
- 嵌入的模块定义代码不能使用 import 加载到其他模块。只有通过外部文件加载的模块才可以使用 import 加载。  
  因此，嵌入模块只适合作为入口模块。

#### 模块加载

ECMAScript 6 模块的独特之处在于，既可以通过浏览器原生加载，也可以与第三方加载器和构建工具一起加载。

完全支持 ECMAScript 6 模块的浏览器可以从顶级模块加载整个依赖图，且是异步完成的。  
浏览器会解析入口模块，确定依赖，并发送对依赖模块的请求。  
这些文件通过网络返回后，浏览器就会解析它们的内容，确定它们的依赖，如果这些二级依赖还没有加载，则会发送更多请求。  
这个异步递归加载过程会持续到整个应用程序的依赖图都解析完成。解析完依赖图，应用程序就可以正式加载模块了。

#### 模块行为

ES6 模块默认在严格模式下执行。

#### 模块导出

ES6 模块支持两种导出：命名导出和默认导出。

**命名导出**

- export 关键字用于声明一个值为命名导出
- 导出语句必须在模块顶级，不能嵌套在某个块中。
- 导出时也可以提供别名，别名必须在 export 子句的大括号语法中指定。
- 因为 ES6 命名导出可以将模块作为容器，所以可以在一个模块中声明多个命名导出。

**默认导出**
默认导出（default export）就好像模块与被导出的值是一回事。  
默认导出使用 default 关键字将一个值声明为默认导出，每个模块只能有一个默认导出。

ES6 模块系统会识别作为别名提供的 default 关键字。此时，虽然对应的值是使用命名语法导出的，实际上则会成为默认导出：

```js
const foo = "foo";
// 等同于export default foo;
export { foo as default };
```

#### 模块导入

命名导出和默认导出的区别也反映在它们的导入上。

命名导出可以使用\*批量获取并赋值给保存导出集合的别名，而无须列出每个标识符：

```js
const foo = "foo",
  bar = "bar",
  baz = "baz";
export { foo, bar, baz };

import * as Foo from "./foo.js";
console.log(Foo.foo); // foo
console.log(Foo.bar); // bar
console.log(Foo.baz); // baz
```

要指名导入，需要把标识符放在 import 子句中。使用 import 子句可以为导入的值指定别名：

```js
import { foo, bar, baz as myBaz } from "./foo.js";
console.log(foo); // foo
console.log(bar); // bar
console.log(myBaz); // baz
```

默认导出就好像整个模块就是导出的值一样。可以使用 default 关键字并提供别名来导入。也可以不使用大括号，此时指定的标识符就是默认导出的别名：

```js
// 等效
import { default as foo } from "./foo.js";
import foo from "./foo.js";
```

如果模块同时导出了命名导出和默认导出，则可以在 import 语句中同时取得它们。可以依次列出特定导出的标识符来取得，也可以使用\*来取得：

```js
import foo, { bar, baz } from "./foo.js";
import { default as foo, bar, baz } from "./foo.js";
import foo, * as Foo from "./foo.js";
```

#### 模块转移导出

模块导入的值可以直接通过管道转移到导出。  
此时，也可以将默认导出转换为命名导出，或者相反。

## 工作者线程

### 工作者线程简介

JavaScript 环境实际上是运行在托管操作系统中的虚拟环境。在浏览器中每打开一个页面，就会分
配一个它自己的环境。这样，每个页面都有自己的内存、事件循环、DOM，等等。每个页面就相当于
一个沙盒，不会干扰其他页面。对于浏览器来说，同时管理多个环境是非常简单的，因为所有这些环境都是并行执行的。
使用工作者线程，浏览器可以在原始页面环境之外再分配一个完全独立的二级子环境。这个子环境
不能与依赖单线程交互的 API（如 DOM）互操作，但可以与父环境并行执行代码。

- 工作者线程是以实际线程实现的。
- 工作者线程并行执行。
- 工作者线程可以共享某些内存。  
  工作者线程能够使用 SharedArrayBuffer 在多个环境间共享内容。  
  虽然线程会使用锁实现并发控制，但 JavaScript 使用 Atomics 接口实现并发控制。
  工作者线程与线程有很多类似之处，但也有重要的区别。
- 工作者线程不共享全部内存
- 工作者线程不一定在同一个进程里
- 创建工作者线程的开销更大

#### 工作者线程的类型

1. 专用工作者线程
   专用工作者线程，通常简称为工作者线程、Web Worker 或 Worker，是一种实用的工具，可以让脚本单独创建一个 JavaScript 线程，以执行委托的任务。专用工作者线程，顾名思义，只能被创建它页面使用。
2. 共享工作者线程
   共享工作者线程与专用工作者线程非常相似。主要区别是共享工作者线程可以被多个不同的上下文使用，包括不同的页面。任何与创建共享工作者线程的脚本同源的脚本，都可以向共享工作者线程发送消息或从中接收消息。
3. 服务工作者线程
   服务工作者线程与专用工作者线程和共享工作者线程截然不同。它的主要用途是拦截、重定向和修改页面发出的请求，充当网络请求的仲裁者的角色。

#### WorkerGlobalScope

在网页上，window 对象可以向运行在其中的脚本暴露各种全局变量。  
在工作者线程内部，没有 window 的概念。  
这里的全局对象是 WorkerGlobalScope 的实例，通过 self 关键字暴露出来。

### 专用工作者线程

专用工作者线程是最简单的 Web 工作者线程，网页中的脚本可以创建专用工作者线程来执行在页面线程之外的其他任务。这样的线程可以与父页面交换信息、发送网络请求、执行文件输入/输出、进行密集计算、处理大量数据，以及实现其他不适合在页面执行线程里做的任务（否则会导致页面响应迟钝）

#### 专用工作者线程的基本概念

可以把专用工作者线程称为后台脚本（background script）。  
JavaScript 线程的各个方面，包括生命周期管理、代码路径和输入/输出，都由初始化线程时提供的脚本来控制。  
该脚本也可以再请求其他脚本，但一个线程总是从一个脚本源开始。

**创建专用工作者线程**
创建专用工作者线程最常见的方式是加载 JavaScript 文件。  
把文件路径提供给 Worker 构造函数，然后构造函数再在后台异步加载脚本并实例化工作者线程。  
传给构造函数的文件路径可以是多种形式。

```js
// emptyWorker.js
// 空的JS工作者线程文件

// main.js
console.log(location.href); // "https://example.com/"
const worker = new Worker(location.href + "emptyWorker.js");
console.log(worker); // Worker {}
// 这个例子非常简单，但涉及几个基本概念。
//  emptyWorker.js文件是从绝对路径加载的。根据应用程序的结构，使用绝对URL经常是多余的。
//  这个文件是在后台加载的，工作者线程的初始化完全独立于main.js。
//  工作者线程本身存在于一个独立的JavaScript环境中，因此main.js必须以Worker对象为代理实
// 现与工作者线程通信。在上面的例子中，该对象被赋值给了worker变量。
//  虽然相应的工作者线程可能还不存在，但该Worker对象已在原始环境中可用了。
// 前面的例子可修改为使用相对路径。不过，这要求main.js必须与emptyWorker.js在同一个路径下：
const worker = new Worker("./emptyWorker.js");
console.log(worker); // Worker {}
```

**工作者线程安全限制**
工作者线程的脚本文件只能从与父页面相同的源加载。  
从其他源加载工作者线程的脚本文件会导致错误。

**使用 Worker 对象**
Worker()构造函数返回的 Worker 对象是与刚创建的专用工作者线程通信的连接点。  
它可用于在工作者线程和父上下文间传输信息，以及捕获专用工作者线程发出的事件。

**DedicatedWorkerGlobalScope**  
在专用工作者线程内部，全局作用域是 DedicatedWorkerGlobalScope 的实例。  
因为这继承自 WorkerGlobalScope，所以包含它的所有属性和方法。  
工作者线程可以通过 self 关键字访问该全局作用域。

### 共享工作者进程

共享工作者线程或共享线程与专用工作者线程类似，但可以被多个可信任的执行上下文访问。

### 服务工作者进程

服务工作者线程（service worker）是一种类似浏览器中代理服务器的线程，可以拦截外出请求和缓存响应。  
这可以让网页在没有网络连接的情况下正常使用，因为部分或全部页面可以从服务工作者线程缓存中提供服务。

### 事件循环

JavaScript 为了避免复杂处理（事件锁），使用了单线程。  
要在单线程中实现非阻塞 IO，就要使用事件循环来实现。JS 引擎本身不实现事件循环机制，是通过宿主（浏览器、nodejs）实现的。  
浏览器和 nodejs 中的事件循环有一定的区别

- 执行栈  
  同步代码的执行，按照执行顺序添加到执行栈中
- 事件队列  
  异步代码则会将事件挂起，等待返回结果后放到事件队列中。等主线程空闲，取出事件对应的回调放入执行栈中执行。
- 宏任务和微任务  
  优先级不同，不同的异步任务被分为宏任务和微任务

- 先执行宏任务，然后再执行当前宏任务产生的微任务，再执行宏任务

| **对比项**       | **浏览器事件循环**                                           | **Node.js 事件循环**                                                                                   |
| ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ |
| **阶段划分**     | 无明确阶段划分，仅分宏任务队列和微任务队列                   | 分为 6 个阶段：Timers → Pending → Poll → Check → Close                                                 |
| **宏任务类型**   | `setTimeout`、`setInterval`、I/O 操作、UI 渲染、脚本执行     | `setTimeout`、`setInterval`、`setImmediate`、I/O 操作、关闭回调                                        |
| **微任务类型**   | `Promise.then`、`MutationObserver`、`queueMicrotask`         | `Promise.then`、`process.nextTick`                                                                     |
| **执行顺序**     | 每个宏任务结束后立即执行所有微任务                           | 每个阶段执行完当前队列的**全部宏任务**后，再执行微任务（旧版本）；<br>Node 11+后每个宏任务后执行微任务 |
| **I/O 处理机制** | 由浏览器多线程（网络线程、渲染线程等）处理，回调推入任务队列 | 由 libuv 库通过线程池处理异步 I/O，完成后回调推入事件队列                                              |
| **定时器优先级** | `setTimeout`回调在延迟结束后进入宏任务队列                   | `setImmediate`在 Check 阶段执行，`setTimeout`在 Timers 阶段执行，I/O 中`setImmediate`优先              |
| **渲染时机**     | 微任务执行后可能触发 UI 渲染                                 | 无渲染阶段，主要用于服务端                                                                             |
| **线程模型**     | 单主线程（JS 执行）+ 多辅助线程（网络、渲染等）              | 单主线程（JS 执行）+ libuv 线程池（I/O 处理）                                                          |

#### 细节知识

Node.js 中 process.nextTick 优先级高于微任务  
requestAnimationFrame 既不是宏任务也不是微任务，属于浏览器渲染前的回调，执行时机在微任务之后、UI 渲染之前。

Timers 阶段  
 处理 setTimeout 和 setInterval 回调  
Check 阶段  
 处理 setImmediate 阶段

#### 应用问题

如何优化长时间任务对时间循环的影响

- 使用 Web Worker 拆分计算密集型任务
- 利用 setTimeout 或 requestldilCallback 分片执行

Promise.all 和 Promise.race 的实现原理及区别

- Promise.all 等待所有 Promise 完成  
  用于需要全部任务都完成的场景，如获取所用关键信息
- Promise.race 以第一个完成/拒绝的 Promise 为准  
  用于需要竞速的场景，如镜像选择、让用户取消长时间操作

### ES6 有哪些新特性

1. let、const
2. 箭头函数
3. 模板字符串
4. 解构赋值
5. 默认参数
6. 扩展运算符
7. 类与模块
8. Promise
9. Symbol 和迭代器
10. 新的数据结构：Map、Set
11. 对象属性简写，属性方法简写

### ajax-axios-fetch

#### Ajax

Asynchronous JavaScript and XML，异步的 JS 和 XML  
AJAX 是一种基于 XMLHttpRequest（XHR）对象的异步通信技术，允许浏览器与服务器交换数据并局部更新页面，而无需刷新整个页面。其核心原理是通过 JavaScript 发起 HTTP 请求，处理响应数据后，使用 DOM 操作动态更新网页内容。

1. 创建 XMLHttpRequest 对象
2. 配置请求
3. 设置回调函数
4. 发送请求
5. 处理响应数据

#### Axios

Axios 是一个基于 Promise 的 HTTP 客户端库，封装了 XHR 对象，支持浏览器和 Node.js 环境。它简化了请求配置，并提供了拦截器、自动 JSON 转换、取消请求等高级功能

1. 发送请求
2. 响应数据
3. 请求和响应拦截器
4. 错误处理

#### Fetch

现代的网络请求 API，用于在浏览器中发起 HTTP 请求。它是 XMLHttpRequest 的升级版，提供了更简洁和强大的接口，并且原生支持 HTTP/2 的一些特性

优点：

- 原生支持 Promise
- 提供了请求和响应对象（Request、Response）
- 支持 HTTP/2 流式处理  
   通过 Response.body 获取到原始的响应流

不足：

- 不会自动携带 cookie
- 无法原生取消请求
- 无法原生监控请求进度

### 深拷贝和浅拷贝

浅拷贝：  
只复制对象的第一层属性，如果属性是 引用类型（如对象、数组），则拷贝的是 引用地址，而不是实际的值。

- Object.assign()
- 展开运算符...
- Array.prototype.slice()

深拷贝：  
递归复制对象的所有层级，包括嵌套的引用类型，生成一个 完全独立的新对象。

- JSON.parse(JSON.stringify(obj))
- 递归
- structuredClone()

## OTHER

### for in 和 for of

| **对比维度**         | **`for...in`**                                         | **`for...of`**                                                |
| -------------------- | ------------------------------------------------------ | ------------------------------------------------------------- |
| **遍历对象类型**     | 普通对象、数组等可枚举属性（包括原型链属性）           | 可迭代对象（数组、字符串、Map、Set、TypedArray、NodeList 等） |
| **遍历内容**         | 对象的键名（Key）或数组的索引（字符串形式）            | 可迭代对象的值（Value）                                       |
| **适用数据结构**     | 对象、数组（不推荐用于数组遍历）                       | 数组、字符串、Map、Set 等支持迭代器的数据结构                 |
| **原型链属性处理**   | 会遍历原型链上的可枚举属性，需用 `hasOwnProperty` 过滤 | 仅遍历对象自身的可迭代值，不涉及原型链                        |
| **循环控制语句支持** | 支持 `break`、`continue`                               | 支持 `break`、`continue`                                      |
| **返回值类型**       | 数组索引为字符串（如 `"0"`）                           | 数组元素为原始类型或对象（如 `1`、`{name: 'John'}`）          |
| **顺序保证**         | 不保证顺序（对象属性无序）                             | 按可迭代对象内部顺序遍历（如数组按索引顺序）                  |
| **自定义迭代能力**   | 无                                                     | 可通过实现 `Symbol.iterator` 方法使普通对象可迭代             |

### forEach() 和 map()

forEach()和 map()方法通常用于遍历 Array 元素

forEach()方法：  
返回 undefined  
不能与其他方法链接

map()  
返回一个包含已转换元素的新数组  
可以链接  
性能更好
