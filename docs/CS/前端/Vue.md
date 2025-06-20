# vue

**MVVM模式**
- Model-View-ViewModel,核心是提供对View和VIewModel的双向数据绑定
- Vue提供了MVVM风格的双向数据绑定，核心是MVVM中的VM，ViewModel负责连接View和Model，保证视图和数据的一致性

## Vue 路由

Vue 路由是构建单页面应用(SPA)的核心技术之一，它允许开发者在不刷新页面的情况下实现视图切换和URL管理。  

### Vue 路由的基本原理

Vue路由的核心原理是基于浏览器的History API或Hashchange事件来实现的。  
它通过监听URL变化并匹配对应的路由规则，然后渲染对应的组件来实现页面的切换。  

基于History API的实现：

- 使用浏览器的History API(pushState``replaceState和popstate)
- URL中的路径部分会被修改成对应的路由路径，但不会刷新页面
- Router实例管理路由规则，每个规则包含路径和对应组件
- 路由跳转时，Router实例捕获路径并渲染对应组件到指定位置 

基于Hashchange的实现：

- 当浏览器不支持History API时自动回退使用
- URL中以#开头的哈希部分被解析为路由路径
- 同样通过Router实例管理路由规则和组件渲染

### Vue 路由的两种主要模式

Vue Router提供了两种路由模式：hash模式和history模式。

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

### Vue Router 高级特性

#### 路由懒加载

#### 导航守卫

- 全局守卫
- 路由独享守卫
- 组件内守卫

完整的导航解析流程：
1. 导航被触发
2. 调用失活组件的`beforeRouteLeave`
3. 调用全局`beforeEach`
4. 调用重用组件的`beforeRouteUpdate`
5. 调用路由配置的`beforeEnter`
6. 解析异步路由组件
7. 调用激活组件的`beforeRouteEnter`
8. 调用全局`beforeResolve`
9. 导航被确认
10. 调用全局`afterEach`
11. 触发DOM更新
12. 调用`beforeRouteEnter`的next回调

#### 动态路由

Vue Router支持运行时动态添加/删除路由：

```javascript
// 添加路由
router.addRoute({ path: '/about', component: About })

// 删除路由
const removeRoute = router.addRoute(routeRecord)
removeRoute() // 删除

// 或通过名称删除
router.removeRoute('about')

// 添加嵌套路由
router.addRoute({ name: 'admin', path: '/admin', component: Admin })
router.addRoute('admin', { path: 'settings', component: AdminSettings })
```

### Vue Router

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

## Vue2 与 Vue3 核心区别对比表

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

### 响应式原理对比（Object.defineProperty与Proxy的对比）

#### Vue2 Object.defineProperty

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

#### Vue3 基于 Proxy  

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

## Vue 的生命周期

Vue 生命周期是指 Vue 组件实例从创建到销毁的完整过程。  

### 为什么需要声明周期

声明周期本质上是 Vue 组件使用流程中的特点时间点，这些时间点分割出了几个阶段，这几个阶段中有一些重要的特性，让部分操作时需要在不同阶段去执行。  
所以 Vue 给出了生命周期的 API，我们了解生命周期的原理就是为了在适合的时间执行适合的操作。

### Vue 生命周期的四个主要阶段

Vue 组件的生命周期可以分为四个主要阶段，每个阶段包含两个钩子函数(一前一后)：

1. **创建阶段(Creation)**：组件实例的初始化过程
   - beforeCreate
   - created

2. **挂载阶段(Mounting)**：将组件挂载到 DOM 的过程
   - beforeMount
   - mounted

3. **更新阶段(Updating)**：响应数据变化并重新渲染的过程
   - beforeUpdate
   - updated

4. **销毁阶段(Destruction)**：组件实例销毁的过程
   - beforeUnmount(Vue 3)/beforeDestroy(Vue 2)
   - unmounted(Vue 3)/destroyed(Vue 2)

此外，Vue 还提供了 `errorCaptured` 钩子用于错误捕获，以及 `renderTracked` 和 `renderTriggered`(仅开发模式)用于调试。

### 每个生命周期的特点

#### 1. 创建阶段

**beforeCreate**
- 在实例初始化之后数据观测(data observation)和事件/侦听器配置之前被调用
- 此时组件实例刚被创建，`data``methods``computed`等选项还未初始化
- 组合式 API 的 `setup()` 会在所有选项式 API 钩子之前调用，包括 beforeCreate

**created**
- 在实例创建完成后被立即调用
- 此时已完成以下配置：数据观测(data observation)、属性和方法的运算watch/event 事件回调
- `data` 和 `methods` 已初始化完成，可以访问
- 但挂载阶段还未开始，`$el` 属性尚不可用
- 常用于异步数据获取初始化非响应式变量等操作

#### 2. 挂载阶段

**beforeMount**
- 在挂载开始之前被调用，相关的 `render` 函数首次被调用
- 此时已完成模板编译，但尚未将组件挂载到 DOM 上
- 在服务端渲染(SSR)时不会被调用

**mounted**
- 在组件挂载完成后调用
- 组件被视为已挂载的条件：
  - 所有同步子组件都已被挂载(不包含异步组件或 `<Suspense>` 树内的组件)
  - 其自身的 DOM 树已创建并插入父容器中
- 可以访问到渲染后的 DOM，常用于操作 DOM初始化第三方库等
- 在服务端渲染时不会被调用
- 注意：不保证所有子组件也都一起被挂载，如果需要等待整个视图都渲染完毕，可以在内部使用 `this.$nextTick()`

#### 3. 更新阶段

**beforeUpdate**
- 在数据更改导致的虚拟 DOM 重新渲染和打补丁之前调用
- 适合在更新之前访问现有 DOM，比如手动移除已添加的事件监听器
- 可以在这个钩子中进一步更改状态，而不会触发附加的重渲染过程
- 在服务端渲染时不会被调用

**updated**
- 在数据更改导致的虚拟 DOM 重新渲染和打补丁之后调用
- 组件 DOM 已经更新，可以执行依赖于 DOM 的操作
- 注意：**不要**在这个钩子中更改状态，这可能会导致无限的更新循环！
- 对于需要对特定状态变化做出反应的情况，最好使用计算属性或 watcher 代替
- 父组件的 updated 钩子将在其子组件的 updated 钩子之后调用

#### 4. 销毁阶段

**beforeUnmount(Vue 3)/beforeDestroy(Vue 2)**
- 在卸载/销毁组件实例之前调用
- 此时实例仍然完全可用，可以在这里进行清理操作
- 常用于清除定时器取消事件监听取消网络请求等
- 在服务端渲染时不会被调用

**unmounted(Vue 3)/destroyed(Vue 2)**
- 在组件实例卸载/销毁后调用
- 组件被视为已卸载的条件：
  - 其所有子组件都已经被卸载
  - 所有相关的响应式作用(渲染作用计算属性侦听器)都已停止
- 可以执行最终的清理工作，但不能再访问组件实例

#### 5. 错误捕获

**errorCaptured**
- 当捕获到来自后代组件的错误时被调用
- 接收三个参数：错误对象触发错误的组件实例错误来源信息的字符串
- 可以返回 `false` 阻止错误继续向上传播
- 错误来源可能包括：组件渲染事件处理器生命周期钩子setup()函数等

### 使用场景

#### 1. 数据请求

- **created**：适合发起异步数据请求，此时数据观测已建立，能更快获取到数据并触发视图更新
- **mounted**：如果需要访问 DOM 才能发起的请求(如基于元素尺寸的请求)，则在此处发起

#### 2. DOM 操作

- **mounted**：是执行 DOM 操作的最安全位置，此时 DOM 已完全渲染
- **updated**：如果需要在数据变化后操作更新后的 DOM，但要注意避免无限循环

#### 3. 清理工作

- **beforeUnmount**：清除定时器取消事件监听断开 WebSocket 连接等
- 避免在 `unmounted` 中执行重要清理，因为此时可能已无法访问所有必要数据

#### 4. 性能优化

- 避免在 `updated` 中修改状态，这会导致额外的重新渲染
- 对于计算量大的操作，考虑使用 `watch` 或计算属性替代生命周期钩子

#### 5. 父子组件生命周期顺序

- 加载时：父 beforeCreate → 父 created → 父 beforeMount → 子 beforeCreate → 子 created → 子 beforeMount → 子 mounted → 父 mounted
- 更新时：父 beforeUpdate → 子 beforeUpdate → 子 updated → 父 updated
- 销毁时：父 beforeUnmount → 子 beforeUnmount → 子 unmounted → 父 unmounted


## 虚拟 DOM

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

### Diff 算法实现原理

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
  
## 如何实现双向绑定？原理？

使用 ref 来新建双向绑定对象  

### 核心原理

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

### 实现流程

1. 初始化
  数据劫持  
  依赖收集  
2. 编译阶段
  指令解析  
  事件监听  
3. 更新阶段
  派发更新  
  虚拟 DOM 优化

## computed 和 watch 的区别

### computed

它根据响应式数据的变化自动重新计算值  

特点：   
- 缓存机制  
  只有当其依赖的响应式数据发生变化时，计算属性才会重新计算。  
- 声明式  
- 同步计算  
- 必须有返回值  

### watch

watch允许你指定一个或多个响应式数据，并对这些数据的变化执行自定义的操作。  
- 无缓存  
  watch不会缓存结果，每次指定的数据变化时，都会执行相应的操作。  
- 命令式  
- 支持异步  
- 不强制返回值  

"computed和watch都是Vue响应式系统的重要组成部分，但定位不同。computed是计算属性，用于派生新数据，具有缓存机制且必须同步返回结果；watch是侦听器，用于响应数据变化执行副作用操作，支持异步且无缓存。  
例如，购物车总价适合用computed，而搜索请求适合用watch。在实现上，computed通过依赖追踪和缓存优化性能，而watch提供了更灵活的变化响应机制。"

## 组件间通信

在不同组件之间传递数据、消息

### `props` and `emit`

最常用的方法，在父子组件之间传递。

props：  
- 父组件向子组件传递数据，单向，子组件不能修改，支持类型校验、默认值设置

emit：  
- 子组件通过 `emit` 定义事件，并发送触发的事件和数据来传递消息，父组件通过 `v-on` 监听事件和数据

### `ref`/`$ref`

父组件通过 ref 获取子组件实例，直接调用子组件的方法或访问数据。
```vue
<Child ref="child" />
<script>
this.$refs.child.methodName();
</script>
```

### `parent`/`children`

通过 $parent 访问父组件实例，$children 访问子组件数组。但这种方式破坏了组件封装性，不推荐频繁使用

### Event Bus（全局事件总线）

创建一个空的 Vue 实例作为事件中心，通过 $emit 发送事件，$on 监听事件

```js

// event-bus.js
export const EventBus = new Vue();
// 组件A发送事件
EventBus.$emit('event-name', data);
// 组件B接收事件
EventBus.$on('event-name', (data) => { ... });

```

### 全局状态管理工具

pinia

### provide/inject 机制

Vue3 的 Provide/Inject 机制是一种跨层级组件通信的解决方案，允许父组件向任意深度的子孙组件直接传递数据，避免了通过 props 逐层传递的繁琐。  

### `attrs`/`listener`

$attrs 包含父组件传递的非 props 属性，$listeners 包含父组件的事件监听器，可跨级传递给子组件。  


## 为什么 data 属性是一个函数而不是一个对象

可以在每次创建新组件实例时返回全新对象，确保每个组件实例有一个独立的数据作用域  

## v-if 和 v-show 有什么区别？使用场景是什么

v-show  
    通过 CSS display 属性来显示或隐藏元素，无论条件是否为真，都会被渲染到 DOM 中  
    会触发 CSS 过渡效果
    频繁切换显示/隐藏状态的场景  
    
v-if  
    通过条件决定是否渲染元素，如果条件为否，不会被渲染到 DOM 中  
    要配合 vue 的 transition 组件过渡  
    不频繁切换的场景  

## slot

### slot 是什么有什么用

插槽是 Vue 实现内容分发的 API，通过 `<slot>` 元素作为承载分发内容的出口。 
插槽的核心作用是：父组件在组件标签内插入任意内容，子组件内通过插槽控制这些内容的摆放位置。  

可以类比为 JavaScript 函数：  

```js
// 父元素传入插槽内容
FancyButton('Click me!')

// FancyButton 在自己的模板中渲染插槽内容
function FancyButton(slotContent) {
  return `<button class="fancy-btn">
      ${slotContent}
    </button>`
}

```

- 默认插槽  
    只有一个插槽  
- 具名插槽
    一个组件多个插槽  
- 作用域插槽
    允许父组件使用子组件提供的数据  
- 条件插槽  
- 动态插槽  

## 渲染模板时，如何保留模板中的 HTML 注释

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
## 如何设计弹窗组件

1. 组件结构，模板、脚本、样式
2. 显示与隐藏逻辑
3. 过渡效果  
    vue 提供的 transition 组件可以实现淡入淡出的效果  
4. 插槽（slot），为弹窗内容提供灵活扩展性
5. 事件处理
6. 样式

## v-cloak v-pre 有什么作用

### v-cloak  

主要用来防止闪烁，在 vue 完全编译前，将绑定的 DOM 元素添加 display：none 样式，避免未解析模板直接显示  

```html
<style>
[v-cloak] { display: none; }
</style>

<div v-cloak>
{{ message }}
</div>
```

### v-pre  

跳过该节点及其子节点的编译过程，直接输出原始的 Mustache 标签（插值符号{{}}）  
提高性能有一定帮助  

```html
<div v-pre>
  {{ rawMustache }}  <!-- 这里的内容将会直接输出为 {{ rawMustache }} 而不是进行数据绑定 -->
</div>
```

## 过滤器

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

## 如何配置 404 页面

使用 * 通配符（匹配所有未定义路径） + NotFound 组件  
**要放在最后**

## 如何实现复杂的表单验证和提交逻辑

- 使用组件（element plus）
- VeeValidate、Yup 工具  
- 非空、正则表达式

## 如何解决页面请求接口大规模并发问题

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


## Vue 中的 nextTick

- Vue 的 `nextTick` 是一个核心 API，用于在 DOM 更新完成后执行延迟回调。
- 它是 Vue 响应式系统中处理异步 DOM 更新的关键机制。

### 为什么需要 `nextTick`

**Vue 的响应式系统的异步更新队列机制**
当你修改数据时，Vue 不会立即更新 DOM，而是开启一个队列，缓冲在同一事件循环中发生的所有数据变更。如果同一个 watcher 被多次触发，只会被推入队列一次。这种去重机制避免了不必要的计算和 DOM 操作。

```js

this.message = '修改后的值1'
this.message = '修改后的值2'
this.message = '修改后的值3'
console.log(vm.$el.textContent) // 仍然显示'原始值'

```

Vue 这个特性提高了效率但也带来了一个问题，DOM 树更新时序的混乱。比如上面代码想要获取更新后的值，但 DOM 树是异步更新的。
所以提供了 `nextTick` 这个 API 来提供在更新后立刻执行相关操作。  

### `nextTick` 的一些机制

Vue 的 nextTick 实现基于 JavaScript 的事件循环(Event Loop)机制，本质是对原生微任务(microTask)和宏任务(macroTask)的封装。其核心实现包括：

- 回调队列：所有 nextTick 回调被存入一个数组(callbacks 或 queue)中
- 异步调度：通过 pending 或 isFlushing 标志防止重复调度
- 降级策略：根据浏览器支持情况选择最优的异步调度方式

### 具体使用

- 操作更新后的 DOM
- 生命周期中的使用
- 当使用 v-if 或 v-show 切换组件时，在组件完全挂载后执行操作

### `nextTick` 与 `setTimeout`

虽然 setTimeout(fn, 0) 也能实现类似效果，但 nextTick 有显著优势：

- 执行时机更早：nextTick 会优先使用微任务，比 setTimeout 的宏任务执行更早
- 性能更好：避免多余的 UI 渲染，因为浏览器会在微任务执行后渲染前执行所有微任务 
- 跨平台兼容：Vue 已经处理了不同浏览器的兼容性问题