# HTML

## 基础知识

### 定义

回流  
当render tree中的一部分或全部因为元素的规模尺寸、布局、隐藏等改变时，浏览器重新渲染部分DOM或全部DOM的过程。回流也被称为重排，其实从字面上来看，重排更容易让人形象易懂（即重新排版整个页面）。

重绘  
当页面元素样式改变不影响元素在文档流中的位置时（如background-color，border-color，visibility），浏览器只会将新样式赋予元素并进行重新绘制操作。

### DOM

Document Object Model, 文档对象模型  

- 元素（element）  
  文档中的所有标签都是元素，元素可以看成是对象  
- 节点（node）  
  文档中所有的内容都是节点：标签，属性，文本  
- 文档（document）  
  一个页面就是一个文档  

文档包含节点，节点包含元素  

#### 对 DOM 树的操作

```js

// 取：  
document.getElementById();

// 获取节点所有属性  
node.attributes  

// 获取节点所有子元素  
node.childNodes  

// 增：  
let a = createElement('a')
document.body.append(a)

// 删：
document.body.removeChild(div);

```

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

innerText会触发回流，但是textContent可能不会触发回流，所以实际应用中，使用textContent性能更佳  
innerTTML会返回HTML文本，textContent的内容不会解析成HTML文本，使用textContent可以防止XSS攻击  

## 面试

### URL 到 页面渲染

1. URL 解析  
  1. 提取协议、主机名、端口号、路径等信息。  
  2. DNS 查询  
2. 建立 TCP 连接  
3. 发送 HTTP 请求和服务器处理  
4. 浏览器解析与渲染流程  
5. JavaScript 执行与交互  
6. 断开 TCP 连接  

### 怎么渲染 http 文件到页面上

1. 构建 DOM 树  
2. 构建 CSSOM 树  
3. 生成渲染树  
4. 布局与绘制  

### 白屏问题的常见原因和排查

1. 网络和资源加载  
  页面资源未加载或加载超时  
  排查：  
    控制台打印错误、网络面板  
    测试CDN与资源路径  
    优化加载策略  
2. 前端代码错误  
3. 服务器与接口问题
4. 浏览器兼容与缓存问题  
5. 第三方服务异常

### js 的加载方式

同步加载  
  浏览器遇到 `<script>` 标签时，会暂停 HTML 解析，下载并执行脚本，完成后才继续渲染页面。  

异步加载
  defer  
  async  
  动态创建  

模块化加载  
  type="module"  

延迟加载  
  import()

### JavaScript 加载冲突

- 命名空间污染导致冲突  
  - 变量、函数名重复  
  - 第三方库冲突  
- 事件绑定冲突  
- 资源加载顺序问题  
- 浏览器兼容性冲突  
- DOM 和资源操作冲突  

### src 和 href

src 是要加载资源的路径  
href 是指定超链接目标地址 或 定义文档与外部资源的关联  

### 性能优化

#### SRC

- 异步加载脚本：  
  - async 属性能让脚本与 HTML 解析并行加载，加载完后立即执行。  
  - defer 属性能让脚本与 HTML 解析并行加载，但执行顺序与页面解析顺序一致，且在解析完成后执行。  
- 图片懒加载：  
  loading="lazy"  
- CDN  
- 资源压缩  

#### href

- 预加载关键资源  
  使用`<link rel='preload' href='style.css' as='style'>`指定关键资源，提高页面加载速度。  
- 防止阻塞渲染  
  将非关键 CSS 文件标记为延迟加载，`media='print' onload="this.media='all';"`  
- 动态加载  
  使用 JS 动态创建 `<link>` 标签加载非必要资源



### preload 和 prefetch

web 加载原语(如<link rel= preload > & <link rel= prefetch >)  

- preload 是一个声明式 fetch，可以强制浏览器在不阻塞 document 的 onload 事件的情况下请求资源。  
- Prefetch 告诉浏览器这个资源将来可能需要，但是什么时间加载这个资源是由浏览器来决定的。  

### Polyfill

Polyfill 是一块代码（通常是 Web 上的 JavaScript），用来为旧浏览器提供它没有原生支持的较新的功能。  

#### 打补丁的三种方法

https://zhuanlan.zhihu.com/p/71640183

1. 手动打补丁  
2. 根据覆盖率自动打补丁
3. 根据浏览器特性，动态打补丁

