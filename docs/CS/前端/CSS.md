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

用于定义元素的显示（如何在页面上布局和显示）  
| 属性值             | 作用描述                                                                  |
| ------------------ | ------------------------------------------------------------------------- |
| **`block`**        | 元素显示为块级元素，独占一行，可设置宽高。默认宽度撑满父容器。            |
| **`inline`**       | 元素显示为行内元素，不换行，不可设置宽高（宽高由内容决定）。              |
| **`inline-block`** | 元素显示为行内块，可设置宽高，但不会独占一行（兼具块级和行内特性）。      |
| **`none`**         | 元素不显示，且不占据文档流空间（完全隐藏）。                              |
| **`flex`**         | 元素变为弹性容器，子元素可通过弹性布局控制排列方式（一维布局）。          |
| **`grid`**         | 元素变为网格容器，子元素可通过网格布局控制行列分布（二维布局）。          |
| **`table`**        | 元素显示为表格（类似 `<table>`），可配合 `table-row`、`table-cell` 使用。 |
| **`list-item`**    | 元素显示为列表项（类似 `<li>`），通常与 `list-style` 属性配合使用。       |
| **`inherit`**      | 继承父元素的 `display` 属性值。                                           |
| **`initial`**      | 设置为默认值（通常是 `inline`）。                                         |
| **`contents`**     | 元素自身不渲染，但其子元素提升到父级层级（常用于隐藏容器但保留内容）。    |

### flex

```css
display: flex;

/* 主轴方向 */
  flex-direction: row;            /* 默认值：从左到右 */
  /* flex-direction: row-reverse; */ /* 从右到左 */
  /* flex-direction: column; */      /* 从上到下 */
  /* flex-direction: column-reverse; */ /* 从下到上 */

/* 换行方式 */
flex-wrap: nowrap;

/* 主轴对齐方式 */
jusity-content: flex-start;

/* 交叉轴对齐方式 */
align-items: stretch;

/* 多行对齐方式 */
align-content: stretch;

```

### grid

## float

## 属性

可继承属性
- color
- font
- letter-spacing
- line
- text

不可继承属性
- background
- border
- display
- position
- float
- width
- left
- z-index

inherit 关键字可以明确让某个属性继承其父元素的值  
initial 关键字把属性设置为其默认值  
unset 对于可继承属性 inherit；不可继承属性 = initial  

## 选择器

| 选择器类型         | 语法示例                   | 作用描述                                                               | 优先级权重（数值） |
| ------------------ | -------------------------- | ---------------------------------------------------------------------- | ------------------ |
| **元素选择器**     | `div`                      | 选择所有指定 HTML 标签的元素（如所有 `<div>`）。                       | 1                  |
| **类选择器**       | `.class-name`              | 选择所有具有指定类名的元素（如 `<div class="class-name">`）。          | 10                 |
| **ID 选择器**      | `#id-name`                 | 选择具有指定 ID 的唯一元素（如 `<div id="id-name">`）。                | 100                |
| **属性选择器**     | `[type="text"]`            | 选择具有指定属性和值的元素（如 `<input type="text">`）。               | 10                 |
| **伪类选择器**     | `:hover`                   | 选择元素的特定状态（如鼠标悬停时的状态）。                             | 10                 |
| **伪元素选择器**   | `::before`                 | 选择元素的特定部分（如在元素前插入内容）。                             | 1                  |
| **通配符选择器**   | `*`                        | 选择页面中的所有元素。                                                 | 0                  |
| **后代选择器**     | `div p`                    | 选择某元素内部的所有指定后代元素（如 `<div>` 内的所有 `<p>`）。        | 权重累加（如 1+1） |
| **子元素选择器**   | `div > p`                  | 选择某元素的直接子元素（如 `<div>` 的直接子元素 `<p>`）。              | 权重累加           |
| **相邻兄弟选择器** | `div + p`                  | 选择紧接在某元素后的第一个兄弟元素（如 `<div>` 后的第一个 `<p>`）。    | 权重累加           |
| **通用兄弟选择器** | `div ~ p`                  | 选择某元素后的所有兄弟元素（如 `<div>` 后的所有 `<p>`）。              | 权重累加           |
| **群组选择器**     | `div, .class, #id`         | 同时选择多个元素（如所有 `<div>`、类名 `.class` 和 ID `#id` 的元素）。 | 独立计算，取最高值 |
| **内联样式**       | `<div style="color: red">` | 直接在 HTML 标签内写的样式。                                           | 1000               |
| **`!important`**   | `color: red !important;`   | 强制覆盖其他样式规则（慎用）。                                         | 优先级最高         |

### 伪类和伪元素的区别

伪类（Pseudo-class）：  
用于选择元素的特定状态或条件  
例如用户交互（悬停、点击）或文档结构（第一个子元素）。  
它不创建新元素，而是对现有元素的补充。  
示例：:hover、:active、:nth-child()  

伪元素（Pseudo-element）：  
用于创建不在DOM树中的虚拟元素，并为其添加样式。  
它模拟了一个新的元素，如首字母或前后插入内容。  
示例：::before、::first-line、::selection  

## 优先级

- 内联样式（HTML 元素上的 style）
    每个加 1000 分  
- ID 选择器（#id）
    每个加 100 分  
- 类选择器、属性选择器、伪类选择器（.class、[attr=value]、:hover）  
    每个加 10 分  
- 元素选择器和伪元素选择器（div、::before）  
    每个加 1 分  
- 通配符选择器、后代选择器、子选择器等（*、div p、div > p）  

优先级相同，后出现的样式生效  

## link 和 @import 引用 CSS 的区别

link  
- 在 `<head>` 部分使用
- 在网页加载时立即加载样式表
- 并行进行，性能好  
- 可通过 JavaScript 操作 DOM

@import
- 在 CSS 文件或`<style>`标签内使用
- 在加载包含它的 CSS 文件后加载  
- 加载顺序依赖，速度慢  
- 不易通过 JavaScript 操作  

## 面试

### BFC

Block Formatting Context，块级格式化上下文  
  它决定了元素如何对其内容进行定位和与其他元素的关系和相互作用。  
  BFC是一个独立的渲染区域，它规定了内部元素如何布局，并且与外部元素相互隔离。  

布局规则：   
- 垂直排列  
- 外边距计算  
- 左边缘对齐  
- 不与浮动重叠  
- 高度计算  
- 独立性  

触发BFC  
- float 值不为 none  
- display 值为 inline-box、flex、grid  
- overflow 值部位 visible  

作用：  
- 解决浮动导致的高度塌陷  
- 防止外边距合并  
- 实现自适应两栏布局  
- 防止元素被浮动元素覆盖  

### Canvas 和 SVG 有什么区别

又是用于在网页上绘制图形的技术  
Canvas 是基于像素的即时绘制技术，适合频繁更新和复杂动画  
SVG 是基于矢量的图形格式，适合需要无损缩放和高分辨率的静态图形  

### CSS3 新特性

布局：  
- 容器查询
  允许根据容器尺寸而非视口调整元素样式，实现组件级响应式设计。  
  `@container (width > 600px) { ... }`  
- 子网格与命名区域  
  子网格：嵌套网格可继承父级对齐方式，简化复杂布局代码。  
  命名区域：通过语义化名称定义网格区域，如`grid-template-areas: "header main sidebar"`，提升代码可读性。  
- 动态视口单位  
  新增`dvh`（动态视口高度）、`lvc`（逻辑视口单位）等，适配折叠屏、刘海屏等异形设备  

颜色与视觉效果：  
- 广色域与 HDR 支持  
  新增`oklch()`、`color(display-p3)`等函数，支持P3色域和HDR显示设备。  
  HWB颜色模型：hwb(0 0% 30%)直接定义色调、白度与黑度，更符合人类直觉。  
- 颜色混合与函数扩展  
  `color-mix()`:混合两种颜色并控制比例，如color-mix(in srgb, red 40%, blue)  
  `@property`：注册自定义颜色属性，支持动画与类型验证  
- 背景滤镜  
  对元素背景区域应用模糊、对比度等滤镜，增强视觉层次感。  

交互与动画：  
- 滚动驱动动画（Scroll-Driven Animations）  
  动画进度与滚动深度绑定，如animation-timeline: scroll()实现视差效果  
- 视图过渡  
  跨文档或单页应用切换时生成平滑动画，支持多页面无缝跳转  
    语法：`::view-transition-old`和`::view-transition-new`控制过渡状态   
- CSS Toggles
  无JavaScript实现状态切换，如暗黑模式：`toggle-root: theme [light dark]`  

响应式与逻辑控制：  
- 逻辑属性  
- `:has()` 选择器  
- 媒体查询扩展  

作用域与模块化  
- `@scope`规则  
- 原生嵌套语法  

