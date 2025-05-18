# express

## 相关文章

[express](https://bakersean168.github.io/2025/05/12/CS/nodejs/express%E4%BD%93%E9%AA%8C/)

## 基础知识

### 中间件

一切皆中间件  

常见的请求参数解析、cookie解析、日志打印等，都可以通过中间件来完成。  

在Express中，中间件是一个函数，它可以访问：  
- 请求对象（req）
- 响应对象（res）
- next函数（指向下一个中间件的函数）
```js
function middleware(req, res, next) {
    // 中间件逻辑
    next(); // 调用下一个中间件
}
```

#### 全局中间件

使用 app.use()

#### 路由中间件

## 模板引擎

模板引擎允许在静态模板文件中使用特定的语法来插入动态内容。  
在运行时，模板引擎会将模板文件转换成 HTML 页面。  

常用模板引擎  
- EJS
- Pug
- Handlebars