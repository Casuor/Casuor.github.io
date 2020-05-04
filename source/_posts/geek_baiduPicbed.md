---

title: BaiduCloud Picbed
categories: Geek
photos: https://cdn.jsdelivr.net/gh/Casuor/CDN/Posts/Image/Extra/20180825/baidupicbed.jpg
date: 2018-8-25

---

## 百度下载图片链：

<https://image.baidu.com/search/down?tn=download&url=><u>巴拉巴拉.jpg</u>

![1555939483530](http://b.hiphotos.baidu.com/image/pic/item/80cb39dbb6fd526669091c42a518972bd4073641.jpg)

## 抓接口

> 首先我们打开百度识图的首页，按 `F12` 呼出浏览器开发者工具，切换到 `Netnork` 选项卡。因为百度识图在上传完图片后会立即进行跳转，因此还需勾选 `Preserve log` 用以保留跳转前的数据。

> 准备就绪后点击 `识图一下 > 本地上传`，随意上传一张图片，这时浏览器 `Netnork` 里会列出在此期间产生的所有网络请求。我们可以点击工具栏里的 `XHR`，用以筛选出数据交互请求。(注：有时用 `XHR`也可能会过滤掉我们需要的数据，因此如果在 `XHR` 中找不到的时候，可以切回 `ALL` 里一个个找)

清空log,Ctrl+R刷新

通过缩略图发现

![1555939791762](<http://f.hiphotos.baidu.com/image/pic/item/35a85edf8db1cb1334741d45d354564e92584b42.jpg>)

得到：

> Request URL: 
> 
> http://g.hiphotos.baidu.com/image/pic/item/37d12f2eb9389b5021eedd048b35e5dde7116e56.jpg

在筛选后的数据请求里，有个名称为 `a_upload?fr=html5&target=pcSearchImage&needJson=true`的请求很是可疑，因此点开查看请求详情。

可以看到，本地的图片果然是通过这个接口进行上传的。上传表单的文件 `name` 为 “file"。接口地址如下：

> http://image.baidu.com/pcdutu/a_upload?fr=html5&target=pcSearchImage&needJson=true

访问结果：

```javascript
{"errno":-1,"msg":"no file","type":"img-upload"}
```

> 解析：错误；
> 
> 错误问题：nofile; 类型：上传文件

至此，我们成功抓取到了百度识图的图片上传接口，接下来可以正式搞事情了

看来，接口没问题

## 写代码

用代码实现很容易，就一个简单的 CURL 上传文件，这里直接给出完整版的代码了，收好！

```php
<?php

/**
 * 上传图片到百度识图接口，获取图片外链
 * 
 * @param     $file 图片文件
 * @return    图片链接(上传成功)    NULL(上传失败)
 * @copyright (c) mengkun(https://mkblog.cn/1619/)
 */
function uploadToBaidu($file) {
    // API 接口地址
    $url = 'http://image.baidu.com/pcdutu/a_upload?fr=html5&target=pcSearchImage&needJson=true';

    // 文件不存在
    if(!file_exists($file)) return '';

    // POST 文件
    if (class_exists('CURLFile')) {     // php 5.5
        $post['file'] = new CURLFile(realpath($file));
    } else {
        $post['file'] = '@'.realpath($file);
    }

    // CURL 模拟提交
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL , $url);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
    curl_setopt($ch, CURLOPT_POST, 1);
    curl_setopt($ch, CURLOPT_POSTFIELDS, $post);
    $output = curl_exec($ch);
    curl_close($ch);

    // 返回结果为空（上传失败）
    if($output == '') return '';

    // 解析数据
    $output = json_decode($output, true);
    if(isset($output['url']) && $output['url'] != '') {
        return $output['url'];
    }
    return '';
}

// 使用示例：
$url = uploadToBaidu('1.jpg');
echo $url;
```
