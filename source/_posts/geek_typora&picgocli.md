---

title: Typora and PicGo-Core Custom cli
categories: Geek
photos: https://cdn.jsdelivr.net/gh/Casuor/CDN@latest/Posts/Image/Common/socks.png
date: 2020-05-06

---

## PicGo-Core via node package manager (Requires NodeJS runtime)


    npm install picgo -g
    picgo --help
    picgo use



    cd .\.picgo\
    cat .\config.json
    


    {
      "picBed": {
        "current": "github",
        "uploader": "github",
        "github": {
          "repo": "GithubName/RepoName",
          "branch": "master",
          "token": "",
          "path": "img/",
          "customUrl": ""
        },
        "transformer": "path"
      },
      "picgoPlugins": {}
    }


## typora custom cli

### windows

![image-20200630120636413](https://raw.githubusercontent.com/Casuor/ImgCDN/master/img/image-20200630120636413.png)

### linux


    which node
    which picgo
    #拼接自定义上传命令如下
    nodepath picgopath upload


