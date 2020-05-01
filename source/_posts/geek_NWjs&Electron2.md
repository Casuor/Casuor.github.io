---
title: 跨平台开发NW.js与Electron(二)
categories: Geek
photos: https://cdn.jsdelivr.net/gh/Casuor/CDN/Posts/Image/Extra/20191228/Electron.png
date: 2019-12-29
---

## 为桌面应用搭建基础架构
### 工序
>构建用户使用路径
>创建线框图
>编写测试
>更新线框图
>编码
>确认应用工作正确

### 安装
    npm install nw
    npm install electron

### 创建工作空间(略)
package.json

    cnpm install osenv --save
    cnom install async --save

index.html

    <html>
    <head>
        <title>Lorikeet</title>
        <link rel="stylesheet" href="style.css" />
        <script src="app.js"></script>
    </head>
    <body>
        <template id="item-template">
            <div class="item">
                <img class="icon" />
                <div class="filename"></div>
            </div>
        </template>
        <div id="toolbar">
            <div id="current-folder">
                <script>
                    document.write(getUsersHomeFolder());
                </script>
            </div>
        </div>
        <div id="main-area"></div>
    </body>
    </html>

app.js

    'use strict';
    //cnpm install osenv --save
    //返回个人用户文件夹模块osenv
    //加载osenv模块
    const osenv = require('osenv');
    //加载node.js文件系统模块
    const fs = require('fs');
    //加载async模块和Node.js path模块
    const async = require('async');
    const path = require('path');
    //获取个人用户文件夹路径
    function getUsersHomeFolder() {
        return osenv.home();
    }
    //getFilesInFoler(),获取文件夹下的列表信息
    function getFilesInFoler(folderPath, cb) {
        fs.readdir(folderPath, cb);
    }
    //使用path模块获取文件名
    function inspectAndDescribeFile(filePath, cb) {
        let result = {
            file: path.basename(filePath),
            path: filePath,
            type: ''
        };
        //调用fs.stat会返回一个对象,包含文件类型
        fs.stat(filePath, (err, stat) => {
            if (err) {
                cb(err);
            } else {
                if (stat.isFile()) {
                    result.type = 'file';
                }
                if (stat.isDirectory()) {
                    result.type = 'directory';
                }
                cb(err, result);
            }
        });
    }
    //使用async模块调用异步函数并收集结果
    function inspectAndDescribeFiles(folderPath, files, cb) {
        async.map(files, (file, asyncCb) => {
            let resolvedFilePath = path.resolve(folderPath, file);
            inspectAndDescribeFile(resolvedFilePath, asyncCb);
        }, cb);
    }
    //创建displayFile函数渲染模版实例
    function displayFile(file) {
        const mainArea = document.getElementById('main-area');
        const template = document.querySelector('#item-template');
        let clone = document.importNode(template.content, true);
        clone.querySelector('img').src = `images/${file.type}.svg`;
        clone.querySelector('.filename').innerText = file.file;
        mainArea.appendChild(clone);
    }
    //创建displayFiles函数来显示列表信息
    function displayFiles(err, files) {
        if (err) {
            return alert('对不起,无法显示此文件');
        }
        files.forEach(displayFile); //在displayFiles中将文件信息传递给displayFile函数
    }
    //main(),调用该函数并将用户个人文件夹路径作为参数传递进去,
    //再将获取到的包含所有文件绝对路径的列表在控制台打印出来
    function main() {
        let folderPath = getUsersHomeFolder();
        getFilesInFoler(folderPath, (err, files) => {
            if (err) {
                return alert('对不起,无法加载你的Home');
            }
            inspectAndDescribeFiles(folderPath, files, displayFiles);
        });
    }
    main();

style.css

    body {
        padding: 0;
        margin: 0;
        font-family: 'Helvetica', 'Arial', 'sans';
    }
    #toolbar {
        top: 0px;
        position: fixed;
        background: rgb(12, 59, 97);
        width: 100%;
        z-index: 2;
    }
    #current-folder {
        float: left;
        color: white;
        background: rgba(0, 0, 0, 0.5);
        padding: 0.5em 1em;
        min-width: 10em;
        border-radius: 0.2em;
        margin: 1em;
    }
    #main-area {
        clear: both;
        margin: 2em;
        margin-top: 3em;
        z-index: 1;
    }
    .item {
        position: relative;
        float: left;
        padding: 1em;
        margin: 1em;
        width: 6em;
        height: 6em;
        text-align: center;
    }
    .item .filename {
        padding-top: 1em;
        font-size: 10pt;
    }
