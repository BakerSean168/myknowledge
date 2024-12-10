 | 分类 | 技术 |
| --- | --- |
| 编程语言 | 低级语言：Assembly, C<br>高级语言：Python, Java, C++, C#, JavaScript, Ruby, PHP, Swift, Kotlin, Go, Rust, TypeScript, Dart |
| 前端开发 | 框架和库：React, Angular, Vue.js, Svelte<br>工具：Webpack, Babel, npm, Yarn<br>CSS：Sass, Less, Tailwind CSS, Bootstrap |
| 后端开发 | 框架：Spring Boot, Django, Flask, Express.js, Ruby on Rails, ASP.NET, Laravel<br>语言：Java, Python, JavaScript (Node.js), Ruby, PHP, C#, Go |
| 数据库 | 关系型数据库：MySQL, PostgreSQL, Oracle, SQL Server<br>非关系型数据库：MongoDB, Cassandra, Redis, CouchDB<br>图数据库：Neo4j |
| 云计算 | 服务提供商：AWS, Google Cloud Platform, Microsoft Azure, IBM Cloud<br>技术：Docker, Kubernetes, OpenStack, Terraform, Ansible |
| DevOps | CI/CD：Jenkins, Travis CI, CircleCI, GitLab CI<br>监控：Prometheus, Grafana, Nagios, ELK Stack (Elasticsearch, Logstash, Kibana)<br>版本控制：Git, GitHub, GitLab, Bitbucket |
| 操作系统 | 桌面：Windows, macOS, Linux (Ubuntu, Fedora, Debian)<br>移动：Android, iOS<br>嵌入式：FreeRTOS, VxWorks, Zephyr |
| 网络与安全 | 网络协议：TCP/IP, HTTP/HTTPS, FTP, DNS<br>安全技术：SSL/TLS, Firewalls, VPN, IDS/IPS, Encryption (AES, RSA), OAuth, JWT |
| 人工智能与机器学习 | 框架和库：TensorFlow, PyTorch, Keras, Scikit-learn, OpenCV<br>技术：深度学习, 强化学习, 自然语言处理 (NLP), 计算机视觉 |
| 数据科学与大数据 | 工具和框架：Hadoop, Spark, Kafka, Flink<br>语言：Python, R, SQL<br>可视化：Tableau, Power BI, Matplotlib, Seaborn |
| 区块链 | 平台：Ethereum, Hyperledger, Bitcoin<br>技术：智能合约, DApps, 加密货币 |
| 虚拟化与容器化 | 虚拟化：VMware, Hyper-V, KVM<br>容器化：Docker, Kubernetes, OpenShift |
| 物联网 (IoT) | 平台：Arduino, Raspberry Pi, ESP8266/ESP32<br>协议：MQTT, CoAP, Zigbee, LoRaWAN |
| 图形与游戏开发 | 引擎：Unity, Unreal Engine, Godot<br>图形库：OpenGL, DirectX, Vulkan |
| 量子计算 | 平台：IBM Q, Google Quantum AI, Microsoft Quantum<br>语言：Qiskit, Cirq, Q# |

# 跨平台框架

Electron  Tauri  Flutter  Qt  

## 跨平台框架比较

| 框架 | 优点 | 缺点 | 适用场景 |
| --- | --- | --- | --- |
| Electron | - 使用 HTML、CSS 和 JavaScript 构建跨平台桌面应用<br>- 大量现成的库和工具<br>- 强大的社区支持 | - 应用体积大<br>- 内存和 CPU 占用高 | - 需要快速开发跨平台桌面应用<br>- 需要使用现有的 Web 技术栈 |
| Tauri | - 体积小，资源占用低<br>- 使用 Rust 构建，性能高<br>- 与前端框架（如 Vue、React）集成良好 | - 生态系统较新，社区和文档不如 Electron 丰富 | - 需要高性能和小体积的跨平台桌面应用<br>- 需要与现代前端框架集成 |
| Flutter | - 使用 Dart 语言，性能高<br>- 单一代码库支持多平台（iOS、Android、Web、桌面）<br>- 丰富的组件和工具 | - Dart 语言相对较新，学习曲线较陡<br>- 桌面支持相对较新，可能不如移动端稳定 | - 需要构建跨平台移动应用<br>- 需要统一代码库支持多平台 |
| Qt | - 使用 C++ 构建，性能高<br>- 丰富的功能和工具<br>- 支持多平台（桌面、移动、嵌入式） | - 学习曲线较陡<br>- 商业许可费用较高 | - 需要高性能和稳定性的跨平台应用<br>- 需要支持嵌入式设备 |

# Nodejs

Node.js是一个基于V8引擎的JavaScript运行环境

## 镜像源

```
.npmrc 文件

# 华为镜像源
# registry=https://repo.huaweicloud.com/repository/npm/

# npm 官方在中国大陆地区的镜像源 ？ 淘宝新镜像源
registry=https://registry.npmmirror.com/
disturl=https://registry.npmmirror.com/-/binary/node
ELECTRON_MIRROR=https://registry.npmmirror.com/-/binary/electron/
```

## 版本管理器

### nvm

*windows下的node.js版本管理器*

| 命令 | 说明 |
| --- | --- |
| `nvm list` | 查看已经安装的版本 |
| `nvm list installed` | 查看已经安装的版本 |
| `nvm list available` | 查看网络可以安装的版本 |
| `nvm arch` | 查看当前系统的位数和当前nodejs的位数 |
| `nvm install [arch]` | 安装制定版本的node 并且可以指定平台 version 版本号 arch 平台 |
| `nvm on` | 打开nodejs版本控制 |
| `nvm off` | 关闭nodejs版本控制 |
| `nvm proxy [url]` | 查看和设置代理 |
| `nvm node_mirror [url]` | 设置或者查看setting.txt中的node_mirror，如果不设置的默认是 https://nodejs.org/dist/ |
| `nvm npm_mirror [url]` | 设置或者查看setting.txt中的npm_mirror,如果不设置的话默认的是：https://github.com/npm/npm/archive/. |
| `nvm uninstall` | 卸载指定的版本 |
| `nvm use [version] [arch]` | 切换指定的node版本和位数 |
| `nvm root [path]` | 设置和查看root路径 |
| `nvm version` | 查看当前的版本 |

## 软件包管理器的管理器

[corepack](https://nodejs.org/api/corepack.html)

### corepack 常用命令

| 命令 | 说明 |
| --- | --- |
| `corepack enable` | 启用 Corepack 以管理包管理器 |
| `corepack disable` | 禁用 Corepack |
| `corepack prepare [package]@[version] --activate` | 准备并激活指定版本的包管理器（如 Yarn、pnpm） |
| `corepack prepare [package]@[version]` | 准备指定版本的包管理器，但不激活 |
| `corepack use [package]@[version]` | 使用指定版本的包管理器 |
| `corepack shim` | 安装或更新 Corepack 的 shim 脚本 |
| `corepack unshim` | 移除 Corepack 的 shim 脚本 |
| `corepack install` | 安装项目中定义的所有依赖 |
| `corepack run [package]@[version] [command]` | 使用指定版本的包管理器运行命令 |
| `corepack list` | 列出所有已安装的包管理器及其版本 |
| `corepack --version` | 显示 Corepack 的版本 |
| `corepack help` | 显示 Corepack 的帮助信息 |

## 软件包管理器

### npm

npm（Node Packaged Modules）

#### npm 常用命令

| 命令 | 说明 |
| --- | --- |
| `npm init` | 初始化一个新的 npm 项目，并创建一个 `package.json` 文件 |
| `npm install [package]` | 安装指定的 npm 包 |
| `npm install [package] --save` | 安装指定的 npm 包并将其添加到 `dependencies` |
| `npm install [package] --save-dev` | 安装指定的 npm 包并将其添加到 `devDependencies` |
| `npm uninstall [package]` | 卸载指定的 npm 包 |
| `npm update [package]` | 更新指定的 npm 包 |
| `npm list` | 列出当前项目安装的所有 npm 包 |
| `npm list -g` | 列出全局安装的所有 npm 包 |
| `npm outdated` | 列出需要更新的 npm 包 |
| `npm run [script]` | 运行在 `package.json` 中定义的脚本 |
| `npm test` | 运行测试脚本 |
| `npm start` | 运行启动脚本 |
| `npm publish` | 发布 npm 包到 npm 仓库 |
| `npm cache clean --force` | 清理 npm 缓存 |
| `npm config set [key] [value]` | 设置 npm 配置 |
| `npm config get [key]` | 获取 npm 配置 |
| `npm help` | 显示 npm 帮助信息 |
| `npm install -g npm` | 更新npm |

### yarn

#### yarn 常用命令

| 命令 | 说明 |
| --- | --- |
| `yarn init` | 初始化一个新的 yarn 项目，并创建一个 `package.json` 文件 |
| `yarn add [package]` | 安装指定的 yarn 包 |
| `yarn add [package] --dev` | 安装指定的 yarn 包并将其添加到 `devDependencies` |
| `yarn remove [package]` | 卸载指定的 yarn 包 |
| `yarn upgrade [package]` | 更新指定的 yarn 包 |
| `yarn install` | 安装项目中定义的所有依赖 |
| `yarn install --frozen-lockfile` | 使用 `yarn.lock` 文件安装依赖，确保版本一致 |
| `yarn list` | 列出当前项目安装的所有 yarn 包 |
| `yarn global add [package]` | 全局安装指定的 yarn 包 |
| `yarn global remove [package]` | 全局卸载指定的 yarn 包 |
| `yarn global list` | 列出全局安装的所有 yarn 包 |
| `yarn outdated` | 列出需要更新的 yarn 包 |
| `yarn run [script]` | 运行在 `package.json` 中定义的脚本 |
| `yarn test` | 运行测试脚本 |
| `yarn start` | 运行启动脚本 |
| `yarn publish` | 发布 yarn 包到 yarn 仓库 |
| `yarn cache clean` | 清理 yarn 缓存 |
| `yarn config set [key] [value]` | 设置 yarn 配置 |
| `yarn config get [key]` | 获取 yarn 配置 |
| `yarn help` | 显示 yarn 帮助信息 |
| `yarn upgrade-interactive` | 交互式更新依赖包 |

*如果yarn install有误时。可重新install或者清除 重新执行*

#### yarn 版本管理

| 命令 | 说明 |
| --- | --- |
| `npm view yarn versions --json` | 查看yarn历史版本 |
| `npm install yarn@latest -g` | 更新yarn |
| `yarn upgrade v1.21.3` | yarn 升级指定版本 |
| `yarn upgrade v1.21.3` | yarn 降低到指定版本（先卸载，再安装） |

### pnpm

#### pnpm 常用命令

| 命令 | 说明 |
| --- | --- |
| `pnpm init` | 初始化一个新的 pnpm 项目，并创建一个 `package.json` 文件 |
| `pnpm install` 或 `pnpm i` | 安装项目中定义的所有依赖 |
| `pnpm add [package]` | 安装指定的 pnpm 包 |
| `pnpm add [package] --save-dev` 或 `pnpm add [package] -D` | 安装指定的 pnpm 包并将其添加到 `devDependencies` |
| `pnpm remove [package]` | 卸载指定的 pnpm 包 |
| `pnpm update [package]` 或 `pnpm up [package]` | 更新指定的 pnpm 包 |
| `pnpm list` 或 `pnpm ls` | 列出当前项目安装的所有 pnpm 包 |
| `pnpm list -g` 或 `pnpm ls -g` | 列出全局安装的所有 pnpm 包 |
| `pnpm outdated` | 列出需要更新的 pnpm 包 |
| `pnpm run [script]` | 运行在 `package.json` 中定义的脚本 |
| `pnpm test` | 运行测试脚本 |
| `pnpm start` | 运行启动脚本 |
| `pnpm publish` | 发布 pnpm 包到 pnpm 仓库 |
| `pnpm cache clean` | 清理 pnpm 缓存 |
| `pnpm config set [key] [value]` | 设置 pnpm 配置 |
| `pnpm config get [key]` | 获取 pnpm 配置 |
| `pnpm help` | 显示 pnpm 帮助信息 |
| `pnpm install -g [package]` | 全局安装指定的 pnpm 包 |
| `pnpm uninstall -g [package]` | 全局卸载指定的 pnpm 包 |
| `pnpm root -g` | 显示全局安装的 pnpm 包的路径 |

# vue + electron

[基于Vue CLI Plugin Electron Builder来把Vue引入Electron工程](https://juejin.cn/post/6983843979133468708#heading-16) 还有 electron-vue  

```
npm i @vue/cli -g

vue create [name]

cd tasky-vue
vue add electron-builder
```


# 技术栈

**开发框架**
- Vue3 
- SpringBoot SpringMVC
**组件库**
- Vant UI 基于Vue的移动端组件库 React版Zent

**序列化库**
- gson
- fastjson

**打包工具**
- Vite 快
**数据库**
- Mysql
- Mariadb

**Other**
- Nginx
- Redis
- MyBatis MyBatis Plus


# SpringBoot

**web入门**
- Spring Boot将传统Web开发的mvc，json，tomcat等框架整合提供了spring-boot-start-web组件，简化了Web应用配置。
- webmvc为Web开发的基础框架，json为JSON数据解析组件，tomcat为自带的容器以来

**控制器**
- Spring Boot提供了 **@Controller（请求页面和数据）** 和 **@RestController（只请求数据）**两种注解来标识此类负责接收和处理HTTP请求

Model       数据
View        页面
Controller  控制器

1. 用户向 Controller 发送**HTTP请求**
2. Controller 向 Model 请求信息
3. Model 响应信息给 Controller
4. Controller 返回数据给 View
5. View HTTP响应给用户

**路由映射**
- @RequestMapping 注解主要负责URL的路由映射。它可以添加在Controller类或具体的方法上。
- 添加在Controller类上，则对类中所有路由映射都加上此规则；加上方法上，则只对当前方法生效。
- @RequestMapping参数：
    **value**：请求URL的路径，支持URL模板，正则表达式
    **method**：HTTP请求方法
    consumes：请求的媒体类型（Content-Type），如application/json
    produces：相应的媒体类型
    params，headers：请求的参数及请求头的值

**参数传递**
- @RequestParam将请求参数绑定到控制器的方法参数上，传输名和参数名一致可省略
- @PathVaraible：用来处理动态的URL，URL的值可以作为控制器中处理方法的参数
- @RequestBody接收的参数是来自requestBody中，即请求体。一般处理非Content-Type：application/x-www-form-urlencoded编码格式的数据，如application/json

**静态资源访问**
- /static/目录
- 在application.properties中直接定义过滤规则和静态资源位置：
    spring.mvc.static-path-pattern=/static/**
    spring.web.resources.static-locations=classpath:/static/

**文件上传**
- 表单enctype属性规定发送到服务器之前应该如何对表单数据继续进行编码。
- 当表单的enctype="multipart/form-data"时，可以使用MultipartFile获取上传的文件数据，再通过transferTO方法将其写入到磁盘中

**拦截器**
- Spring Boot定义了HandlerInterceptor接口来实现自定义拦截器的功能
- HandlerINterceptir接口定义了preHandle，postHandle，afterCompletion三种方法，通过重写这三种方法实现请求前，请求后等操作

**拦截器注册**
- addPathPatterns方法定义拦截的地址
- excludePathPatterns定义排除某些地址不被拦截
- 添加的一个拦截器没有addPathPattern任何一个url则默认拦截所有请求
- 没有excludePathPattern任何一个url则默认不放过一个请求

**RESRful**
- 每一个URI代表一种资源
- GET获取资源，POST新建资源，PUT更新资源，DELETE删除资源
- 通过操作资源的表现形式来实现服务端请求操作
- 资源的表现形式是JSON或者HTML

**使用Swagger生成WebAPI文档**


#### 注解
@restcontroller
@requestmapping
@PathVaraible
@RequestBody

## HTML

### color
nav
- background-color: #24252A;
- color: #edf0f1;
- box-shadow: 0 1px 5px rgba(0, 0, 0, 0.2);
- link
    - hover: color: #0088a9;

sidebar
- li
    - a
        - color: #0088a9;
        - border: 1px solid #2f2f32;

todolist
- background-color: #333239;
- border: 1px solid #333239;
- box-shadow: #8e6363 1px 1px 10px;
    - ul li
        - background-color: #3e3c45;
        - border: 1px solid #3e3c45;
        - box-shadow: #767676 1px 1px 10px;

button
- background-color: #124477;
- color: #edf0f1;
- &:hover {
        background-color: #156cc6;
      }
- background-color: #801d1d;
- color: #edf0f1;
- &:hover {
        background-color: #aa1111;
      }

#26263e

```
form {
  display: block;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 600px;
  height: 500px;
  background-color: #37383a;
  color: #edf0f1;
  border-radius: 10px;
  padding: 20px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  overflow: hidden;
  .form-item {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
    label {
      font-size: 20px;
    }
    input {
      font-size: 20px;
      border: none;
      border-bottom: 1px solid #ccc;
      padding: 10px;
      outline: none;
      background-color: #37383a;
      color: #b4bec1;
    }
  }
  .form-item-check {
    display: flex;
    justify-content: center;
  }
  h2 {
    text-align: center;
    margin-bottom: 10px;
  }

  .form-button {
    display: flex;
    align-items: center;
    justify-content: space-around;
    margin-top: 50px;
    .form-button-submit {
      width: 100px;
      height: 40px;
      border: none;
      border-radius: 5px;
      background-color: #124477;
      color: #edf0f1;
      font-size: 20px;
      cursor: pointer;
      &:hover {
        background-color: #156cc6;
      }


  }
    .form-button-cancel {
      width: 100px;
      height: 40px;
      border: none;
      border-radius: 5px;
      background-color: #801d1d;
      color: #edf0f1;
      font-size: 20px;
      cursor: pointer;
      &:hover {
        background-color: #aa1111;
      }
    }
  }
}
```



### vue

**MVVM模式**
- Model-View-ViewModel,核心是提供对View和VIewModel的双向数据绑定
- Vue提供了MVVM风格的双向数据绑定，核心是MVVM中的VM，ViewModel负责连接View和Model，保证视图和数据的一致性

**Vue框架**

**Vue组件化**

**生命周期函数**
created
mounted


**Axios网络请求**
- Axios是一个基于promise网络请求库
- Axios只用XMLHttpRequests发送网络请求，并能自动完成JSON数据的转换

**前端路由VueRouter**