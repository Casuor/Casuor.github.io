---
title: Electron Notes
categories: Geek
photos: https://cdn.jsdelivr.net/gh/Casuor/CDN/Posts/Image/Extra/20191228/Electron.png
date: 2019-9-25
---
# Electorn 
## 技术栈
## 环境搭建
1.Node.js

2.Git
[NVM]()
常用命令：
```shell
nvm arch    #版本64or32
nvm install [version] [arch]  #安装
nvm list [available] #显示安装版本或已经安装的版本
nvm on 
nvm off
nvm proxy [url]
nvm node_mirror [url]
nvm npm_mirror[url]
nvm uninstall <version>
nvm use [version] [arch]
nvm root [path]
nvm version
```
npm初始化
```shell
#查看部分配置信息
npm config ls
#修改全局Node moudle位置
初始位置：
prefix = "C:\\Users\\16877\\AppData\\Roaming\\npm"
cache = "C:\\Users\\16877\\AppData\\Roaming\\npm-cache"
修改：
npm config set prefix "F:\Develop_Node.js\Gobal_Npm_Module"
npm config set cache "F:\Develop_Node.js\Gobal_Npm_Cache"
#修改Npm cache位置
```
PS:其他也可以设置

安装cnpm
```shell
npm install -g cnpm --registry=https://registry.npm.taobao.org
#此外需添加环境变量
cnpm -v
```
PS :
problem:
```
 The process cannot access the file because it is being used by another process.
```
方案1：
淘宝镜像
```shell
nvm node_mirror https://npm.taobao.org/mirrors/node/
nvm npm_mirror https://npm.taobao.org/mirrors/npm/ 
```
方案2：
直接下载个exe安装到nvm所指定的路径名称改为(LTS版本：'v12.13.1')

3.Electorn
>(1)克隆示例项目的仓库

```shell
git clone https://github.com/electron/electron-quick-start
```

>(2)进入仓库
```shell
cd electron-quick-start
```

>(3)安装依赖并启动
```shell
cnpm install or npm install
npm start
#使用npm卡住需在.npmrc文件添加
registry=https://registry.npm.taobao.org
electron_mirror="https://npm.taobao.org/mirrors/electron/"
PS:install.js文件中有electron_mirror这一项，使用cnpm没问题
```
[npm地址](http://caibaojian.com/npm/troubleshooting/if-your-npm-is-broken.html)

## 进程和线程 
### 什么是进程
### 什么是线程
### 进程与线程的区别
1.内存使用方面的区别
2.通信机制方面的区别
3.量级方面的区别
## Electorn 主进程和渲染进程
chrom 多进程管理{主进程+渲染进程}
main process
使用和系统对接的Electorn API-创建菜单,创建菜单,上传文件等
创建渲染进程-Render Process
全面支持Node.js
有且只有一个程序入口点
Render Process
可以有多个,每个对应一个窗口
每个都是一个单独的进程
全面支持Node.js和Dom API
可使用部分Electron 进程
[Multi-process Architecture](https://www.chromium.org/developers/design-documents/multi-process-architecture)
## 创建Browser Window
cnpm install --save-dev nodemon
Edit package.json
```json
{
  "name": "electron-quick-start",
  "version": "1.0.0",
  "description": "A minimal Electron application",
  "main": "main.js",
  "scripts": {
    "start": "nodemon --watch main.js --exec electron ."
  },
  "repository": "https://github.com/electron/electron-quick-start",
  "keywords": [
    "Electron",
    "quick",
    "start",
    "tutorial",
    "demo"
  ],
  "author": "GitHub",
  "license": "CC0-1.0",
  "devDependencies": {
    "electron": "^7.1.2",
    "nodemon": "^2.0.1"
  }
}
```
Main.js

```js
// Modules to control application life and create native browser window
//common.js
const {app, BrowserWindow} = require('electron')
app.on('ready', () => { 
  let mainWindow = new BrowserWindow(
    {
      width: 800,
      height: 500,
      webPreferences: {
        nodeIntegration:true
      }
    }
  )
  mainWindow.loadFile('index.html')
})```
