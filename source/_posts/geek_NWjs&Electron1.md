---
title: 跨平台开发NW.js与Electron(一)
categories: Geek
photos: https://cdn.jsdelivr.net/gh/Casuor/CDN/Posts/Image/Extra/20191228/Electron.png
date: 2019-12-25
---


## Node.js桌面应用
### 优势之一
>通常，开发桌面应用要求开发者们精通像C++、Objective-C，或
>者C#这样的语言以及像.NET、Qt、Cocoa或者GTK这样的框架。
>对于部分开发者而言，准入门槛有点高，很可能会放弃使用这些
>技术来构建桌面应用。
>像Electron和NWjs这样的Nodejs桌面应用框架最棒的地方就在于它>们大大降低了开发者的准入门槛。支持开发者使用HTML、CSS和J>avaScript开发桌面应用，而且还可以在Web应用和桌面应用之间
>共享同一份代码，这无异于是给Web开发者打开了一扇通往成为
>桌面应用开发者的门。

### 缘起
#### Reference
##### book:
跨平台桌面应用开发 基于Electron与NW.JS
##### site:
历史细节
[Electron ](http://cheng.guru/blog/2016/05/13/from-node-webkit-to-electron-1-0.html)
[Is Electron originally forked from NW.js, or is it just inspired by NW.js (if so, is it a fork of any existing repository) ?](https://github.com/electron/electron/issues/5172)
两框架对比
[技术差异](https://electronjs.org/docs/development/atom-shell-vs-node-webkit)
[NW.js vs electron](https://tangiblejs.com/posts/nw-js-and-electron-compared-2016-edition)
[NW.js中文网](https://nwjs.org.cn/)
演变
node-webkit--->[NW.js](https://nwjs.io/)
Atom Shell  --->[Electron](https://electronjs.org/)

### NW.js
#### Reference
[Cross Platform Desktop Applications](https://github.com/Casuor/cross-platform-desktop-applications)

#### NW.js介绍
安装NW.js

    cnpm install -g nw

构建hello-world应用
package.json

    {
      "name" : "hello world nwjs",
      "main" : "index.html",
      "version" : "1.0.0"
    }

index.html

    <html>
      <head>
        <title>Hello World</title>
        <style>
          body {
            background-image: linear-gradient(45deg, #EAD790 0%, #EF8C53 100%);
            text-align: center;
          }
          button {
            background: rgba(0,0,0,0.40);
            box-shadow: 0px 0px 4px 0px rgba(0,0,0,0.50);
            border-radius: 8px;
            color: white;
            padding: 1em 2em;
            border: none;
            font-family: 'Roboto', sans-serif;
            font-weight: 100;
            font-size: 14pt;
            position: relative;
            top: 40%;
            cursor: pointer;
            outline: none;
          }
          button:hover {
            background: rgba(0,0,0,0.30);
          }
        </style>
        <link href='https://fonts.googleapis.com/css?family=Roboto:300' rel='stylesheet' type='text/css'>
        <script>
          function sayHello () {
            alert('Hello World');
          }
        </script>
      </head>
      <body>
        <button onclick="sayHello()">Say Hello</button>
      </body>
    </html>

`nw`即可运行

##### NW.js有哪些特性
- 通过JS访问操作系统原生的UI和API

>控制应用视窗的大小和行为
>在应用视窗中显示菜单项的工具条
>在用户右击的时候，在应用视窗中添加上下文菜单。
>在操作系统托盘菜单中添加应用的菜单项。
>访问操作系统的剪贴板，读写其中的内容。
>使用计算机中默认指定的应用打开文件、文件夹以及URL。
>通过操作系统的通知系统显示通知。


- 在应用中使用Node.js和npm应用

>web应用与NW.js开发的桌面应用的区别，后者，前后端代码的界限很模糊，因为同一段JavaScript代码共享了前后端的上下文

[https://github.com/nw-cn/awesome-nwjs](https://github.com/nw-cn/awesome-nwjs)
[https://github.com/sindresorhus/awesome](https://github.com/sindresorhus/awesome)

- 同一份代码构建支持多操作系统的应用
app->npm install -g nw-builder&nwbuild app/->build

#### Electron介绍
Electron是GitHub开发的桌面应用开发框架。它最早的名字叫Atom Shell，是为GitHub的文本编辑器Atom构建的。它支持使用HTML、CSS和JavaScript来构建跨平台的桌面应用。自它2013年11月发布以来，越来越流行，不少创业公司和大公司都纷纷用它来构建他们的桌面应用。不仅Atom在用Electron，连聊天应用Slack（https:/www.slack.com）的桌面客户端应用也在用，这家创业公司截至2016年4月估值已达38亿美金。

##### Electron是如何工作的以及它和NW.js的区别是什么

1.整合chromium和Node.js的方式不同

>在NW.js中,chromium是直接被打补丁打进去的,因此Node.js和chromium共享了同一个JavaScript上下文.
>在electron中而是通过chromium的Content API以及使用了Node.js的node_bindings

2.处理JavaScript上下文时和NW.js不同

>在NW.js中,维护一个共享的JavaScript上下文
>在electron中,多个独立的JavaScript上下文(main&renderer进程)

3.入口不同

>在NW.js中,html文件为入口
>在electron中,js文件为入口

安装Electron

    cnpm install electron
    cnpm install nodemon

构建electron hello world 应用

package.json

    {
      "name": "hello_world",
      "main": "main.js",
      "version": "1.0.0",
      "scripts": {
        "start": "nodemon --watch main.js --exec electron ."
      }
    }

main.js

    'use strict';
    const electron = require('electron');
    const app = electron.app;
    const BrowserWindow = electron.BrowserWindow;
    let mainWindow = null;
    app.on('window-all-closed', () => {
        if (process.platform !== 'darwin') app.quit();
    });
    app.on('ready', () => {
        mainWindow = new BrowserWindow();
        mainWindow.loadURL(`file://${__dirname}/index.html`);
        mainWindow.on('closed', () => {
            mainWindow = null;
        });
    });

index.html 

    同上

    cnpm start 

##### Electron 有哪些特性

支持创建多视窗，而且每个视窗都有自己独立的JavaScript上下文。
通过shell和screenAPI整合了桌面操作系统的特性。
支持获取计算机电源状态。
支持阻止操作系统进入省电模式（对于演示文稿类应用非常有用）。
支持创建托盘应用。
支持创建菜单和菜单项。
支持为应用增加全局键盘快捷键。
支持通过应用更新来自动更新应用代码。
支持汇报程序崩溃。
支持自定义Dock菜单项。
支持操作系统通知。
支持为应用创建启动安装器。

#### NW.js和Electron支持创建哪类应用
**List**
[NW.js APPS](https://github.com/nwjs/nw.js/wiki/List-of-apps-and-companies-using-nw.js)
[Electron APPS](https://github.com/sindresorhus/awesome-electron)

