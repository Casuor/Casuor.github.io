---
title: Node.js Usages-01
categories: Geek
photos: https://cdn.jsdelivr.net/gh/Casuor/CDN/Posts/Image/20191223/nodejs.png
date: 2019-4-20
---
## 安装
### NVM Node管理
[Nvm-windos](https://github.com/coreybutler/nvm-windows)

### 常用命令
![](https://cdn.jsdelivr.net/gh/Casuor/CDN/Posts/Image/20191223/carbon.svg)

### nvm install node problem:

>The process cannot access the file because it is being used by another process.

方案1：
>淘宝镜像

    nvm node_mirror https://npm.taobao.org/mirrors/node/
    nvm npm_mirror https://npm.taobao.org/mirrors/npm/ 


方案2：
>直接下载个exe安装到nvm所指定的路径名称改为(LTS版本：'v12.13.1')

预览:
![](https://cdn.jsdelivr.net/gh/Casuor/CDN/Posts/Image/20191223/nvm_install.png)

## 配置

### npm配置

    #查看配置信息
    npm config ls
    #修改全局Node moudle位置
    初始位置：
    prefix = "C:\\Users\\16877\\AppData\\Roaming\\npm"
    cache = "C:\\Users\\16877\\AppData\\Roaming\\npm-cache"
    修改：
    npm config set prefix "F:\Develop_Node.js\Gobal_Npm_Module"
    npm config set cache "F:\Develop_Node.js\Gobal_Npm_Cache"
    #修改Npm cache位置

PS:其他也可以设置


## 使用cnpm

    npm install -g cnpm --registry=https://registry.npm.taobao.org
    #此外需添加环境变量
    cnpm -v

**PS:**
诸多网速问题，使用cnpm比较好

**类似问题解决方案：**

    cnpm install 
    or 
    npm install
    #使用npm卡住需在.npmrc文件添加（使用 npm config ls可以找到这一项）
    registry=https://registry.npm.taobao.org
    #install.js 卡住也是此类问题，同样设置依赖镜像地址
    #如install electron:
    electron_mirror="https://npm.taobao.org/mirrors/electron/"
**PS:**
install.js文件中有electron_mirror这一项，使用cnpm没问题


## nrm—切换npm源
>nrm 是一个 NPM 源管理器，允许你快速地在如下 NPM 源间切换：

1.安装

    npm install -g nrm

2.使用

    #列出可选的源
    nrm ls
    #查看所有或指定测试源响应时间
    nrm test [name]
    #切换指定源
    nrm use <name>
