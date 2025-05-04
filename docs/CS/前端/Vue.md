# vue

**MVVM模式**
- Model-View-ViewModel,核心是提供对View和VIewModel的双向数据绑定
- Vue提供了MVVM风格的双向数据绑定，核心是MVVM中的VM，ViewModel负责连接View和Model，保证视图和数据的一致性

## Vue Router

Vue Router 是 Vue.js 的官方路由管理器，用于构建单页面应用（SPA），通过动态管理 URL 与组件的映射关系实现无刷新页面切换。  

- 路由映射  
  将 URL路径与 Vue 组件绑定，通过 routes 数组配置  
- 路由出口  
  通过 `<router-view>` 渲染匹配组件， `<router-link>` 生成导航链接  
- 路由模式  
  Hash 模式、History 模式、Memory 模式（适用于非浏览器环境，不依赖 URL）  
- 动态路由与参数  
- 导航方式  
- 重定向与别名  
  配置 redirect 属性  
  alias 属性允许多个路径渲染同一组件  
- 404 处理  
  用通配符路径 `path: '/:pathMatch(.*)*'` 匹配未定义路由，渲染错误页面  
- 路由守卫  
- 懒加载  
- 嵌套路由  
- 
### Hash 模式与 History 模式

#### Hash 

Hash模式是Vue Router的默认模式，它使用URL的hash(即#号及其后面的部分)来模拟完整的URL。  

特点：  
- URL 中包含`#`符号  
- 通过`window.location.hash`获取当前 URL 的 hash 值。  
- 通过`window.onhashchange`监听 hash 值的变化。  
- hash 值不会包含在 HTTP 请求中，对服务器完全无用  
- 每次改变 hash 都会在浏览器访问历史中增加一个记录  
- 兼容性好  

#### History

History模式基于HTML5的History API，提供了更"干净"的URL，没有#符号。  

特点：  
- URL 更直观  
- 使用`history.pushState()`和`replaceState()`方法修改 URL  
- 通过`window.onpopstate`监听路由变化  
- 要服务端支持  
- 需要浏览器支持HTML5 History API，不兼容IE9及以下版本  

### Vue Router 中如何获取路由传递的参数

#### 动态路由匹配

使用`/user/:id`这样的路径来定义一个动态参数路由  
然后通过`this.$route.params`来获取传递的参数   

#### 查询参数

在 URL 中使用查询字符串的形式传参，`/user?id=123`  
然后通过`this.$route.query`来获取传递的参数   


## 面试

- template 标签
    占位符

### Vue2 与 Vue3 核心区别对比表

| 特性                    | Vue2                                                      | Vue3                                                                                        | 引用来源 |
| ----------------------- | --------------------------------------------------------- | ------------------------------------------------------------------------------------------- | -------- |
| **API 设计**            | Options API（逻辑分散在 `data`、`methods` 等选项中）      | Composition API（通过 `setup()` 集中逻辑，支持复用）                                        |          |
| **响应式系统**          | 基于 `Object.defineProperty`（无法检测动态属性/数组索引） | 基于 `Proxy`（支持动态属性、深层嵌套对象/数组监听）                                         |          |
| **生命周期钩子**        | 直接定义（如 `mounted()`）                                | 钩子名前加 `on`（如 `onMounted()`），需显式引入；`setup()` 替代 `beforeCreate` 和 `created` |          |
| **模板根节点**          | 必须单根节点，需外层 `<div>` 包裹                         | 支持多根节点（Fragments）                                                                   |          |
| **TypeScript 支持**     | 需额外配置，类型推断较弱                                  | 原生深度支持，类型推导更完善                                                                |          |
| **性能优化**            | 较慢的虚拟 DOM 和响应式初始化                             | 虚拟 DOM 优化（`patchFlag` 标记静态节点）、Tree-shaking 减少体积、Proxy 响应式性能更优      |          |
| **新组件特性**          | 无                                                        | 新增 `Teleport`（渲染到任意 DOM 节点）、`Suspense`（异步组件加载状态管理）                  |          |
| **全局 API**            | `Vue.use()`、`Vue.component()` 等全局方法                 | 模块化引入（如 `createApp()`），避免全局污染                                                |          |
| **自定义指令**          | 钩子函数如 `inserted`、`update`                           | 钩子名更新（如 `mounted`、`updated`），支持更灵活的生命周期                                 |          |
| **v-model**             | 单个绑定（`value` + `input` 事件）                        | 支持多绑定（如 `v-model:title`），可自定义事件名                                            |          |
| **逻辑复用**            | Mixins（易命名冲突）                                      | 组合式函数（Composables），通过函数封装逻辑                                                 |          |
| **SSR 支持**            | 支持但优化较少                                            | 流式渲染、静态节点优化，性能提升                                                            |          |
| **体积与 Tree-shaking** | 较大，无法按需引入                                        | 更小（约 10KB），支持 Tree-shaking 剔除未使用代码                                           |          |

#### 响应式原理对比（Object.defineProperty与Proxy的对比）

##### Vue2 Object.defineProperty

基本原理：  
Vue 2的响应式系统核心是通过Object.defineProperty来实现数据劫持。  
当我们将一个普通 js 对象传入 Vue 实例作为 data 选项时，Vue 会遍历对象的所有属性，使用 Object.defineProerty 将这些属性转换为 getter/setter。  

工作流程：  
1. 初始化  
2. 依赖收集  
   getter 收集  
3. 派发更新  
  setter 通知依赖更新  

局限性：  
- 无法检测对象属性的新增/删除  
  因为Object.defineProperty只能劫持已存在的属性，新增属性需要使用Vue.set或this.$set  
- 数组监听的限制  
  直接通过索引修改数组(arr[index] = newValue)或修改长度无法被检测，Vue通过重写数组的7个方法(push/pop/shift/unshift/splice/sort/reverse)来实现响应式  
- 性能问题  
  需要对data对象进行深度递归遍历，初始化大型对象时性能较差  

##### Vue3 基于 Proxy  

Vue3 使用 ES6 的 Proxy 全面重构了响应式系统。Proxy 可以拦截对象的基本操作（如属性查找、赋值、枚举等），提供了更强大和灵活的响应式能力。  

Proxy基本机制：  
Proxy构造函数接受两个参数：
target：要代理的目标对象
handler：定义拦截行为的对象

常见拦截操作：  
get(target, prop)：拦截属性读取
set(target, prop, value)：拦截属性设置
deleteProperty(target, prop)：拦截属性删除

优势：  
- 全面拦截  
- 性能优化  
  按需代理，依赖追踪更精细  
- 更好的开发体验  
  不需要使用Vue.set等特殊API  
- 支持更多的数据结构  
  Map、Set 等

### Vue 的生命周期

初始化、挂载、更新、销毁  

- beforeCreate:创建前  
  在beforeCreate阶段，还不能访问data、computed、watch、methods上的方法和数据。  
- created：创建后  
  在created阶段，可以访问data、computed、watch、methods上的方法和数据。不能访问$el等属性  
- beforeMount：挂载前  
  已经把data里的数据和模板生成html，但是还没有把html挂载到界面  
- mounted：挂载后  
  可以正常获取DOM元素 beforeUpdate：更新前，获取不到更新的真实DOM  
- update：更新后  
  获取的是更新的真实DOM beforeDestroy：销毁前（比如采用v-if的方式，移除组件）   
- destroyed：销毁后  

### 虚拟 DOM

虚拟DOM（Virtual DOM）是一种用于优化页面渲染性能的技术，其核心原理是通过 JavaScript 对象对真实DOM进行抽象描述，并作为中间层协调视图更新。  

1. 抽象表示
  虚拟DOM通过轻量级的JS对象（如tagName、props、children等属性）模拟真实DOM结构。例如，一个`<div>`节点会被表示为：
  ```Js
  { tag: 'div', props: { id: 'app' }, children: [...] }
  ```
  这种抽象使得操作成本远低于直接操作真实DOM。
2. 更新流程
  初次渲染：将虚拟DOM转化为真实DOM并挂载到页面。
  状态变更：生成新的虚拟DOM树。
  差异对比（Diff算法）：比较新旧虚拟DOM树的差异。
  批量更新：仅将差异部分应用到真实DOM，减少重绘和回流。
3. 核心优势
  性能优化：通过批量更新减少DOM操作次数。
  跨平台能力：虚拟DOM可适配不同平台（如Web、Native），只需实现对应的渲染逻辑。
  开发友好性：开发者无需手动优化DOM操作。

#### Diff 算法实现原理

Diff算法是虚拟DOM的核心，用于高效找出新旧虚拟DOM树的差异。其核心策略包括：  
1. 分层比较  
  仅比较同一层的节点，如果节点跨层移动，直接删除旧节点，创建新节点。  
2. 双端对比（Vue）  
  头头、尾尾、头尾、尾头 匹配，减少遍历次数。  
3. Key 的作用  
  通过唯一 key 标识节点身份，避免复用导致顺序错乱。  
  列表渲染中，可帮助 Diff 快速定位可复用节点。  
4. 动态节点标记（Vue3 优化）
  Vue3在编译阶段通过patchFlag标记动态节点（如绑定响应式变量的元素），运行时直接定位变更部分，跳过全树对比。  
  
### 如何实现双向绑定？原理？

使用 ref 来新建双向绑定对象  

#### 核心原理

1. 劫持数据对象的属性读写操作，建立响应式系统。
  Vue 3.x：改用Proxy代理整个对象，支持深层监听和数组操作，性能更优  
  ```js
  const proxy = new Proxy(obj, {
    get(target, key) { track(target, key); },  // 依赖收集
    set(target, key, value) { 
      trigger(target, key);  // 触发更新
      return Reflect.set(target, key, value);
    }
  });
  ```
2. 发布-订阅模式  
  通过 Dep 和 Watcher 管理依赖关系：  
  - Dep 每个被劫持的属性关联一个 Dep 实例，负责存储所有依赖它的 Watcher  
  - Watcher 在组件渲染或计算属性时创建，订阅数据变化，触发视图更新  

#### 实现流程

1. 初始化
  数据劫持  
  依赖收集  
2. 编译阶段
  指令解析  
  事件监听  
3. 更新阶段
  派发更新  
  虚拟 DOM 优化

### computed 和 watch 的区别

#### computed

它根据响应式数据的变化自动重新计算值  

特点：   
- 缓存机制  
  只有当其依赖的响应式数据发生变化时，计算属性才会重新计算。  
- 声明式  
- 同步计算  
- 必须有返回值  

#### watch

watch允许你指定一个或多个响应式数据，并对这些数据的变化执行自定义的操作。  
- 无缓存  
  watch不会缓存结果，每次指定的数据变化时，都会执行相应的操作。  
- 命令式  
- 支持异步  
- 不强制返回值  

"computed和watch都是Vue响应式系统的重要组成部分，但定位不同。computed是计算属性，用于派生新数据，具有缓存机制且必须同步返回结果；watch是侦听器，用于响应数据变化执行副作用操作，支持异步且无缓存。  
例如，购物车总价适合用computed，而搜索请求适合用watch。在实现上，computed通过依赖追踪和缓存优化性能，而watch提供了更灵活的变化响应机制。"

### provide/inject 机制

Vue3 的 Provide/Inject 机制是一种跨层级组件通信的解决方案，允许父组件向任意深度的子孙组件直接传递数据，避免了通过 props 逐层传递的繁琐。  


### 为什么 data 属性是一个函数而不是一个对象

可以在每次创建新组件实例时返回全新对象，确保每个组件实例有一个独立的数据作用域  

### v-if 和 v-show 有什么区别？使用场景是什么

v-show  
    通过 CSS display 属性来显示或隐藏元素，无论条件是否为真，都会被渲染到 DOM 中  
    会触发 CSS 过渡效果
    频繁切换显示/隐藏状态的场景  
    
v-if  
    通过条件决定是否渲染元素，如果条件为否，不会被渲染到 DOM 中  
    要配合 vue 的 transition 组件过渡  
    不频繁切换的场景  

### slot

slot 是什么有什么用

是一种用于在组件模板中分发内容的机制。  
用它来将父组件的内容传递给子组件,从而实现灵活的内容分发和复用  

- 默认插槽  
    只有一个插槽  
- 具名插槽
    一个组件多个插槽  
- 作用域插槽
    允许父组件使用子组件提供的数据  
- 条件插槽  
- 动态插槽  

### 渲染模板时，如何保留模板中的 HTML 注释

默认情况下不会保留，但可以使用 v-html 指令实现  

```html

<template>
  <div v-html="htmlContent"></div>
</template>

<script>
export default {
  data() {
    return {
      htmlContent: '<!-- This is an HTML comment -->'
    };
  }
};
</script>

```
### 如何设计弹窗组件

1. 组件结构，模板、脚本、样式
2. 显示与隐藏逻辑
3. 过渡效果  
    vue 提供的 transition 组件可以实现淡入淡出的效果  
4. 插槽（slot），为弹窗内容提供灵活扩展性
5. 事件处理
6. 样式

### v-cloak v-pre 有什么作用

#### v-cloak  

主要用来防止闪烁，在 vue 完全编译前，将绑定的 DOM 元素添加 display：none 样式，避免未解析模板直接显示  

```html
<style>
[v-cloak] { display: none; }
</style>

<div v-cloak>
{{ message }}
</div>
```

#### v-pre  

跳过该节点及其子节点的编译过程，直接输出原始的 Mustache 标签（插值符号{{}}）  
提高性能有一定帮助  

```html
<div v-pre>
  {{ rawMustache }}  <!-- 这里的内容将会直接输出为 {{ rawMustache }} 而不是进行数据绑定 -->
</div>
```

### 过滤器

用于格式化显示文本、日期、货币等  
用 method 实现  

```javascript
export default {
  methods: {
    capitalize(value) {
      if (!value) return '';
      value = value.toString();
      return value.charAt(0).toUpperCase() + value.slice(1);
    }
  }
}
```
```html
<p>{{ capitalize(message) }}</p>
```

### 如何配置 404 页面

使用 * 通配符（匹配所有未定义路径） + NotFound 组件  
**要放在最后**

### 如何实现复杂的表单验证和提交逻辑

- 使用组件（element plus）
- VeeValidate、Yup 工具  
- 非空、正则表达式

### 如何解决页面请求接口大规模并发问题

- 前端并发控制  
    请求合并  
    请求队列  
    防抖节流：对频发请求进行控制  
- 数据缓存  
    前端缓存：利用浏览器缓存、local storage 等机制缓存数据  
    接口缓存：合理设置 HTTP 缓存头、利用 CDN 缓存  
- 服务端优化  
    数据库优化  
    服务端缓存  
    负载均衡  
