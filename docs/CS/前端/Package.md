## 镜像源

```
.npmrc 文件

## 华为镜像源
## registry=https://repo.huaweicloud.com/repository/npm/

## npm 官方在中国大陆地区的镜像源 ？ 淘宝新镜像源
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