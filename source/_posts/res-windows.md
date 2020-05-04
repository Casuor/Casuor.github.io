---
title: Windows的奇技淫巧
categories: Resource
photos: https://cdn.jsdelivr.net/gh/Casuor/CDN/Posts/Image/Extra/20191228/win10.png
date: 2019-10-28
---



[TOC]

## 浏览器

[Chrome](https://www.google.com/chrome/)

[EDGE](https://www.microsoft.com/en-us/edge)

[Firefxo](https://www.firefox.com.cn/download/)

## 通信

[telegram](https://www.microsoft.com/zh-cn/p/telegram-desktop/9nztwsqntd0s#activetab=pivot:overviewtab)

### TG群
[reference1](http://suo.im/6ebJiI)
[reference2](http://suo.im/5Jqvy9)
## 截图

[Snipaste](https://docs.snipaste.com/zh-cn/)

## 视频播放器

[Potplayer](https://potplayer.org/)
[爱奇艺万能联播](http://mbdapp.iqiyi.com/j/ot/GeePlayerSetup_app.exe)
[MPC-HC](https://mpc-hc.org/)
## 网络电视
[ZY Player](https://github.com/Hunlongyu/ZY-Player)
[柠檬影视]()

## 在线视频(大都是个人维护,易失效,这类网站巨多)
[919yy影视](https://vod.919yy.com/)
[在线影视](https://www.zxzj.me/)

## 音频播放器

Groove
[MusicPlayer](https://github.com/zhongyang219/MusicPlayer2)

## 音乐播放器

网易云音乐&[解锁灰色歌曲](https://zhuanlan.zhihu.com/p/79631291)
`QQ音乐`

## 系统工具

[Dism++](https://www.chuyu.me/zh-Hans/)

[Windows10Manager](http://www.carrotchou.blog/2561.html)

[Geek Uninstaller](https://geekuninstaller.com/download)

[360驱动大师](http://weishi.360.cn/qudongdashi/index.html)

## 图像处理

`泼辣修图||PhotoShop`

## 图床工具

[PicGo](https://molunerfinn.com/PicGo/)

配合Github搭建自己的[CDN](https://www.jsdelivr.com/)

## 录屏&Gif

`班迪录屏`&[screentogif](https://www.screentogif.com/)

## Office

[OfficeTool](https://otp.landian.vip/zh-cn/)

## 系统下载激活工具

[microsoft-iso-downloader](http://softwarez.us/microsoft-iso-downloader-pro-2020-2-2/)

建议配合IDM使用

## 下载工具

[IDM](https://www.qiuziyuan.net/pcrj/zcjh/2018-05-17/348.html)

## 搜索工具

[Everything](https://www.voidtools.com/zh-cn/)

[UTools](https://u.tools/)

## 输入法

[手心输入法](http://xinshuru.com/index.html?p=win)

[Rime](https://rime.im/)

## 办公同步协作

[石墨文档](https://www.seafile.com/home/)

[seafile](https://www.seafile.com/home/)

## PDF阅读器&编辑器

[sumatrapdf](https://www.sumatrapdfreader.org/free-pdf-reader.html)

[MovaviPDF Editor](https://www.qiuziyuan.net/pcrj/image/940.html)

## 思维导图

`Xmind`

`Mindmaster`

## 护眼软件

`护眼宝`

## 手机控制电脑

`Hipc`

## OCR识别工具

[**天若OCR文字识别**](https://github.com/AnyListen/tianruoocr/releases)

## 远程控制

`TeamViewer`

## 电子书转换

[Calibre](https://calibre-ebook.com/download_windows)

[cloudconvert](https://cloudconvert.com/)

PS:[电子书下载](https://casuor.top/2019/09/26/res-books/)

## 文档下载

<img src="https://cdn.jsdelivr.net/gh/Casuor/CDN/Posts/Image/Extra/20191228/doc.jpg" style="zoom:50%;" />

## Markdown 编辑器

`Typora`

`Sublime Text 3`

## 图表工具

[Draw.io](https://www.draw.io/)

PS:有UWP版的

`Microsoft Whiteboard`

[https://tableconvert.com/](https://tableconvert.com/)

## 文件云同步

`onedrive`(教育版5T)

PS:[配合RaiDrive使用](https://shimo.im/docs/jytKgDY9hQthCcWp/)

`坚果云`

## 磁力工具

[FDM](https://www.freedownloadmanager.org/zh/)

`WebTorrent Desktop`

基于 node.js、WebRTC  的开源技术，任何人都可以通过 Github 获取源码并搭建一个视频网站 😂 然而这个太折腾了。
[https://webtorrent.io/desktop/](https://webtorrent.io/desktop/)

如果碰到无法播放的情况

[https://instant.io/](https://instant.io/)

## 批处理工具

去除快捷方式角标


    reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Icons" /v 29 /d "%systemroot%\system32\imageres.dll,197¡å /t reg_sz /f
    taskkill /f /im explorer.exe
    attrib -s -r -h "%userprofile%\AppData\Local\iconcache.db"
    del "%userprofile%\AppData\Local\iconcache.db" /f /q
    start explorer
    pause


去除小盾牌


    reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Icons" /v 29 /d "%systemroot%\system32\imageres.dll,197" /t reg_sz /f
    reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Icons" /v 77 /d "%systemroot%\system32\imageres.dll,197" /t reg_sz /f
    taskkill /f /im explorer.exe
    attrib -s -r -h "%userprofile%\AppData\Local\iconcache.db"
    del "%userprofile%\AppData\Local\iconcache.db" /f /q
    start explorer
    +


## 美化工具

[致美化](https://zhutix.com/)

PS:先看教程再使用

[Wallhaven Wallpaper](https://wallhaven.cc/)

PS:[如何爬取wallhaven图片](https://casuor.top/2019/12/21/geek-wallhavenspider/)

## TODO

`Microsoft TODO`

