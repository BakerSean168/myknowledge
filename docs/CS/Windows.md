
## environment

### node.js
#### 管理器
**nvm**
常用命令
nvm list	查看已经安装的版本
nvm list installed	查看已经安装的版本
nvm list available	查看网络可以安装的版本
nvm arch	查看当前系统的位数和当前nodejs的位数
nvm install [arch]	安装制定版本的node 并且可以指定平台 version 版本号 arch 平台
nvm on	打开nodejs版本控制
nvm off	关闭nodejs版本控制
nvm proxy [url]	查看和设置代理
nvm node_mirror [url]	设置或者查看setting.txt中的node_mirror，如果不设置的默认是 https://nodejs.org/dist/
nvm npm_mirror [url]	设置或者查看setting.txt中的npm_mirror,如果不设置的话默认的是：https://github.com/npm/npm/archive/.
nvm uninstall	卸载指定的版本
nvm use [version] [arch]	切换指定的node版本和位数
nvm root [path]	设置和查看root路径
nvm version	查看当前的版本


### python
#### 管理器
**virtualenv**
create
virtualenv --python route env_name
run
.\env_name\Scripts\activate
stop
deactivate

#### 打包器

py2exe
Nuitka
pyinstall