---
title: Wallhaven Spider
categories: Geek
photos: https://cdn.jsdelivr.net/gh/Casuor/CDN/Posts/Image/20191221/geek.png
date: 2019-12-21
---

## reference

https://www.cnblogs.com/simple-li/p/11202461.html

说明:初学Python,目前再啃廖雪峰的教程

额,这个写的有点问题,所以以下是改造吧,额不使用`lxml`也是可以的,就简单的拼接字符串问题,但效率可能慢点

#### other

[lxml](https://www.cnblogs.com/zhangxinqi/p/9210211.html)

[etree的用法](https://www.jb51.net/article/161053.htm)

python中去除字符串中空白字符的最简单方法


    string="hello world  "
    string.replace(" ","")

[delete blank](https://www.cnblogs.com/zhanghengyu/p/11121160.html)

## Problem

1.文件下载进程随时会出现假死状态,需要大改,并封装一下搜索下载,美滋滋

2.`pychram`控制台接收一个输入的网址,回车自动跳到浏览器

## 分析

​	1.文件读写

​	2.抓包,解析文件地址

​	3.下载文件

## 实现代码

    # 爬取某网站的壁纸图片
    import os
    import random
    
    import requests
    from lxml import etree
    import time
    
    # 伪装浏览器
    headers = {
        "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5)AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.104 Safari/537.36",
    }


    # 定义创建文件路径函数，将下载的文件存储到该路径
    def CreatePath(filepath):
        if not os.path.exists(filepath):
            os.makedirs(filepath)


    # 获取壁纸首页网页信息并解析
    def getUrlText(url):
        respons = requests.get(url, headers=headers)  # 获取网页信息
        urlText = respons.text
        html = etree.HTML(urlText)  # 使用lxml解析网页
        return html


    # 提取壁纸链接地址列表
    def getWallUrl(url):
        hrefUrl = getUrlText(url)
        section = hrefUrl.xpath('//section[@class="thumb-listing-page"]')[0]  # 获取section标签
        hrefList = section.xpath('./ul//@href')  # 获取首页图片对应链接地址
        return hrefList


    # 获取当前时间
    def getTime():
        nowtime = time.strftime('%Y-%m-%d %H:%M:%S', time.localtime(time.time()))
        return nowtime


    # 解析壁纸下载地址
    def downWall(url, page):
        '''
        :param url: 网页地址
        :param page: 下载页数
        :return: 下载结束提醒
        '''
        global i, n
        m = 0
        page += 1
        for i in range(1, page):
    
            hrefList = getWallUrl(url + str(i))
            print('第' + str(i) + '页')
            print(hrefList)
            n = 0
            print('开始下载第{}页壁纸'.format(i))
            for href in hrefList:
                n += 1
                imgUrl = getUrlText(href)  # 获取壁纸链接网页信息并解析
                imgSrc = imgUrl.xpath('//img[@id="wallpaper"]/@src')[0].strip()
                print(imgSrc)
    
                try:
                    res = requests.get(imgSrc)
                    print(res, res.status_code)
                    pic_path = '/wallpaper/Picture/' + imgSrc[31:]
                    print(pic_path)
                    with open(pic_path, 'wb') as f:
                        f.write(res.content)
                        f.close()
                    print('{}:第{}页第{}张壁纸下载完成'.format(getTime(), i, n))
                    time.sleep(random.uniform(0, 3))
    
                except Exception as e:
                    print(repr(e))
            m = m + n
        return print('{}:所有壁纸已下载完成，一共{}页{}张'.format(getTime(), i, m))


    # url = 'https://wallhaven.cc/search?q=id%3A711&ref=fp&tdsourcetag=s_pcqq_aiomsg&page='
    def main():
        filepath = ('/wallpaper/Picture/')  # 存储路径。
        page = int(input('请输入你想下载的页数:'))
        CreatePath(filepath)
        downWall('https://wallhaven.cc/search?q=id%3A3799&page=', page)


    if __name__ == '__main__':
        main()
