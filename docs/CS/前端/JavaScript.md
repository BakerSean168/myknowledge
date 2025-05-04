# JavaScript

https://www.bookstack.cn/read/javascript-tutorial/README.md

## 简单知识

### 特点

单线程、非阻塞异步处理机制

### 数据类型

原始类型  
- 数值（number）：整数和小数（比如1和3.14）
- 字符串（string）：文本（比如Hello World）。
- 布尔值（boolean）：表示真伪的两个特殊值，即true（真）和false（假）
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

### == 和 ===

JavaScript 中的 ==（宽松相等）和 ===（严格相等）是两种不同的比较运算符，核心区别在于 是否进行类型转换 以及 对特殊值的处理规则

### 执行上下文

- 全局执行上下文：全局执行环境是最外围的一个执行环境，在浏览器的全局对象是 window, this指向这个对象。  
- 函数执行上下文：可以有无数个，函数被调用的时候会被创建。每次调用函数都会创建一个新的执行上下文。  
- eval执行上下文，很少用。  

每个执行上下文，都有三个重要属性：  
- 变量对象 (variable object, VO)  
    每个执行环境都有一个与之关联的变量对象，环境中定义的所有变量和函数都保存在这个对象中。虽然我们编写的代码无法访问这个对象，但解析器在处理数据时会在后台使用它。  
- 作用域链（scope chain）  
    当代码在一个环境中执行时，会创建变量对象的一个作用域链。作用域链的用途，是保证对执行环境有权访问的所有变量和函数的有序访问。  
- this  
    普通函数指向函数的调用者：有个简便的方法就是看函数前面有没有点，如果有点，那么就指向点前面的那个值;  
    箭头函数指向函数所在的所用域：注意理解作用域，只有函数的{}构成作用域，对象的{}以及 if(){}都不构成作用域;  

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

### 作用域

JavaScript中的作用域(Scope)是指程序中定义变量的区域，它决定了变量和函数的可访问性和生命周期。  

- 全局作用域  
  脚本模式运行所有代码的默认作用域  
- 模块作用域  
  模块模式中运行代码的作用域  
- 函数作用域  
  由函数创建的作用域
- 块作用域（用 let 或 const 声明的变量属于）  
  解决了es5存在的2个重要问题  
    - 内层变量覆盖外层变量  
    - 循环计数变量泄露为全局变量  

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
  return function(...args) {
    clearTimeout(timer);
    timer = setTimeout(() => {
      func.apply(this, args);
    }, delay);
  };
}

//支持立即执行版本
function debounce(func, delay, immediate = false) {
  let timer;
  return function(...args) {
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
  return function(...args) {
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
  return function(...args) {
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
  let last = 0, timer;
  return function(...args) {
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

### 事件循环

JavaScript 为了避免复杂处理（事件锁），使用了单线程。  
要在单线程中实现非阻塞IO，就要使用事件循环来实现。JS引擎本身不实现事件循环机制，是通过宿主（浏览器、nodejs）实现的。  
浏览器和 nodejs 中的事件循环有一定的区别  

- 执行栈  
  同步代码的执行，按照执行顺序添加到执行栈中  
- 事件队列  
  异步代码则会将事件挂起，等待返回结果后放到事件队列中。等主线程空闲，取出事件对应的回调放入执行栈中执行。  
- 宏任务和微任务  
  优先级不同，不同的异步任务被分为宏任务和微任务  

- 先执行宏任务，然后再执行当前宏任务产生的微任务，再执行宏任务

| **对比项**       | **浏览器事件循环**                                           | **Node.js事件循环**                                                                                    |
| ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ |
| **阶段划分**     | 无明确阶段划分，仅分宏任务队列和微任务队列                   | 分为6个阶段：Timers → Pending → Poll → Check → Close                                                   |
| **宏任务类型**   | `setTimeout`、`setInterval`、I/O操作、UI渲染、脚本执行       | `setTimeout`、`setInterval`、`setImmediate`、I/O操作、关闭回调                                         |
| **微任务类型**   | `Promise.then`、`MutationObserver`、`queueMicrotask`         | `Promise.then`、`process.nextTick`                                                                     |
| **执行顺序**     | 每个宏任务结束后立即执行所有微任务                           | 每个阶段执行完当前队列的**全部宏任务**后，再执行微任务（旧版本）；<br>Node 11+后每个宏任务后执行微任务 |
| **I/O处理机制**  | 由浏览器多线程（网络线程、渲染线程等）处理，回调推入任务队列 | 由libuv库通过线程池处理异步I/O，完成后回调推入事件队列                                                 |
| **定时器优先级** | `setTimeout`回调在延迟结束后进入宏任务队列                   | `setImmediate`在Check阶段执行，`setTimeout`在Timers阶段执行，I/O中`setImmediate`优先                   |
| **渲染时机**     | 微任务执行后可能触发UI渲染                                   | 无渲染阶段，主要用于服务端                                                                             |
| **线程模型**     | 单主线程（JS执行）+ 多辅助线程（网络、渲染等）               | 单主线程（JS执行）+ libuv线程池（I/O处理）                                                             |

#### 细节知识

Node.js中process.nextTick优先级高于微任务  
requestAnimationFrame 既不是宏任务也不是微任务，属于浏览器渲染前的回调，执行时机在微任务之后、UI渲染之前。

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
AJAX是一种基于XMLHttpRequest（XHR）对象的异步通信技术，允许浏览器与服务器交换数据并局部更新页面，而无需刷新整个页面。其核心原理是通过JavaScript发起HTTP请求，处理响应数据后，使用DOM操作动态更新网页内容。  

1. 创建 XMLHttpRequest 对象  
2. 配置请求
3. 设置回调函数
4. 发送请求
5. 处理响应数据

#### Axios

Axios是一个基于Promise的HTTP客户端库，封装了XHR对象，支持浏览器和Node.js环境。它简化了请求配置，并提供了拦截器、自动JSON转换、取消请求等高级功能  

1. 发送请求  
2. 响应数据  
3. 请求和响应拦截器  
4. 错误处理

#### Fetch

现代的网络请求 API，用于在浏览器中发起 HTTP 请求。它是 XMLHttpRequest 的升级版，提供了更简洁和强大的接口，并且原生支持 HTTP/2的一些特性  

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

### 常用函数、方法、对象

#### Array

##### 数组常用方法表格总结

| 方法名                                     | 作用                              | 返回值                         | 示例                                     |
| ------------------------------------------ | --------------------------------- | ------------------------------ | ---------------------------------------- |
| **`push(item)`**                           | 在数组末尾添加元素                | 新数组长度                     | `arr.push(5);` → 长度+1                  |
| **`pop()`**                                | 删除并返回最后一个元素            | 被删除元素                     | `const last = arr.pop();`                |
| **`unshift(item)`**                        | 在数组开头添加元素                | 新数组长度                     | `arr.unshift(0);` → 长度+1               |
| **`shift()`**                              | 删除并返回第一个元素              | 被删除元素                     | `const first = arr.shift();`             |
| **`splice(start, deleteCount, ...items)`** | 在指定位置增删/替换元素           | 被删除元素的数组               | `arr.splice(1, 1, 'a');` → 替换索引1元素 |
| **`slice(start, end)`**                    | 截取数组片段（不修改原数组）      | 新数组                         | `const sub = arr.slice(0, 2);`           |
| **`indexOf(item)`**                        | 查找元素首次出现的索引            | 索引（未找到返回 `-1`）        | `arr.indexOf('apple');` → 0 或 -1        |
| **`find(callback)`**                       | 返回满足条件的第一个元素          | 元素（未找到返回 `undefined`） | `arr.find(x => x > 5);`                  |
| **`filter(callback)`**                     | 返回满足条件的所有元素的新数组    | 新数组                         | `arr.filter(x => x % 2 === 0);`          |
| **`map(callback)`**                        | 遍历处理元素并返回新数组          | 新数组                         | `arr.map(x => x * 2);`                   |
| **`forEach(callback)`**                    | 遍历执行操作（无返回值）          | `undefined`                    | `arr.forEach(x => console.log(x));`      |
| **`reduce(callback, initialValue)`**       | 累加处理数组元素                  | 最终累加结果                   | `arr.reduce((sum, x) => sum + x, 0);`    |
| **`sort([compareFn])`**                    | 排序数组（默认按字符串Unicode码） | 排序后的原数组                 | `arr.sort((a, b) => a - b);`             |
| **`reverse()`**                            | 反转数组元素顺序                  | 反转后的原数组                 | `arr.reverse();` → `[3, 2, 1]`           |
| **`concat(arr2)`**                         | 合并多个数组                      | 新数组                         | `const merged = arr1.concat(arr2);`      |
| **`join(separator)`**                      | 将数组转为字符串（指定分隔符）    | 字符串                         | `arr.join(', ');` → `"a, b, c"`          |
| **`includes(item)`**                       | 检查是否包含某元素                | 布尔值                         | `arr.includes('apple');` → `true/false`  |
| **`some(callback)`**                       | 检查是否有至少一个元素满足条件    | 布尔值                         | `arr.some(x => x > 10);`                 |
| **`every(callback)`**                      | 检查是否所有元素都满足条件        | 布尔值                         | `arr.every(x => x > 0);`                 |

#### Object

| 方法名                          | 描述                                       | 示例                                                               |
| ------------------------------- | ------------------------------------------ | ------------------------------------------------------------------ |
| `Object.keys(obj)`              | 返回对象自身可枚举属性的键名数组           | `Object.keys({a:1, b:2})` → `["a", "b"]`                           |
| `Object.values(obj)`            | 返回对象自身可枚举属性的键值数组           | `Object.values({a:1, b:2})` → `[1, 2]`                             |
| `Object.entries(obj)`           | 返回对象自身可枚举属性的键值对二维数组     | `Object.entries({a:1, b:2})` → `[["a", 1], ["b", 2]]`              |
| `Object.assign(target, ...src)` | 合并源对象属性到目标对象（浅拷贝）         | `Object.assign({a:1}, {b:2})` → `{a:1, b:2}`                       |
| `Object.create(proto)`          | 创建以指定对象为原型的新对象               | `const obj = Object.create({name: "Alice"}); obj.name` → `"Alice"` |
| `Object.freeze(obj)`            | 冻结对象（不可修改/添加/删除属性）         | `Object.freeze(obj); obj.a = 2` → 修改失败                         |
| `Object.seal(obj)`              | 密封对象（不可添加/删除属性，但可修改值）  | `Object.seal(obj); obj.a = 2` → 修改有效                           |
| `Object.is(val1, val2)`         | 严格值比较（处理 `NaN` 和 `±0`）           | `Object.is(NaN, NaN)` → `true`；`Object.is(0, -0)` → `false`       |
| `Object.fromEntries(entries)`   | 将键值对列表转换为对象                     | `Object.fromEntries([["a",1], ["b",2]])` → `{a:1, b:2}`            |
| `Object.hasOwn(obj, prop)`      | 检查对象自身是否包含指定属性（ES2022新增） | `Object.hasOwn({a:1}, 'a')` → `true`                               |

#### Map

#### Map 常用方法

| 操作类型         | 方法/属性          | 语法示例/描述                                                              | 来源参考 |
| ---------------- | ------------------ | -------------------------------------------------------------------------- | -------- |
| **创建Map**      | `new Map()`        | `const map = new Map();` 或 `new Map([[key1, val1], [key2, val2]])` 初始化 |          |
| **添加键值对**   | `.set(key, value)` | 支持链式调用：`map.set('a', 1).set('b', 2)`                                |          |
| **获取值**       | `.get(key)`        | `map.get('a')` → 返回对应值，不存在返回 `undefined`                        |          |
| **判断键存在**   | `.has(key)`        | `map.has('a')` → 返回布尔值                                                |          |
| **删除键值对**   | `.delete(key)`     | `map.delete('a')` → 成功删除返回 `true`，否则 `false`                      |          |
| **清空Map**      | `.clear()`         | 删除所有键值对：`map.clear()`                                              |          |
| **获取大小**     | `.size`            | 属性直接访问：`map.size` → 返回键值对数量                                  |          |
| **遍历键**       | `.keys()`          | 返回迭代器：`for (let key of map.keys()) { ... }`                          |          |
| **遍历值**       | `.values()`        | 返回迭代器：`for (let val of map.values()) { ... }`                        |          |
| **遍历键值对**   | `.entries()`       | 返回 `[key, value]` 数组迭代器：`for (let [k,v] of map.entries()) { ... }` |          |
| **迭代全部元素** | `.forEach()`       | `map.forEach((value, key) => { ... })`（注意参数顺序为 `值, 键`）          |          |

#### typeof

检查变量类型，返回字符串，表示数据类型  

```js

console.log(typeof undefined); // "undefined"
console.log(typeof true);      // "boolean"
console.log(typeof 42);        // "number"
console.log(typeof "hello");   // "string"
console.log(typeof {});        // "object"
console.log(typeof []);        // "object"
console.log(typeof null);      // "object" (特殊情况)
console.log(typeof function(){}); // "function"
console.log(typeof Symbol());  // "symbol"
console.log(typeof 10n);       // "bigint"

```

主要用于基本数据类型、函数、未定义类型、symbol

#### 遍历对象属性

Object.keys  
Object.getOwnPropertyNames  
Object.entries  
for...in  

#### 读取二进制文件

ArrayBuffer

### API

## 面试

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

forEach()和map()方法通常用于遍历Array元素  

forEach()方法：  
返回 undefined  
不能与其他方法链接   

map()  
返回一个包含已转换元素的新数组  
可以链接  
性能更好  


