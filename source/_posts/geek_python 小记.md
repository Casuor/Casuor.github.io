---

title: python小记(未完)
categories: Geek
photos: https://cdn.jsdelivr.net/gh/Casuor/CDN@latest/Posts/Image/Common/kawayi0.jpg
date: 2019-01-06

---

# python 小记

### 查看python路径

```python
Python

import sys

print(sys.path)
```

![UTOOLS1588859685660.png](http://yanxuan.nosdn.127.net/2cbdeb063ab9178305a3906a43dbba4a.png)

### 设置pip源

C:\Users\16877\pip\pip.ini

```ini
[global]
index-url = http://mirrors.aliyun.com/pypi/simple 

[install]
trusted-host=mirrors.aliyun.com
```

### Github

[Rich](https://github.com/willmcgugan/rich) is a Python library for rich text and beautiful formatting in the terminal. 

![print.png](https://user-gold-cdn.xitu.io/2020/5/9/171f89ef3cf4ca18?w=1844&h=1258&f=png&s=382648)

### Anaconda config

[Anaconda Installer](https://www.anaconda.com/products/individual#windows)

[Anaconda修改国内镜像源](https://www.jianshu.com/p/042fd657e2d4)

```powershell
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/

conda config --set show_channel_urls yes

cd ~
ls
code .\.condarc
```

```
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
show_channel_urls: true
```

```powershell
conda info
```

[Anaconda Usuages](https://docs.conda.io/projects/conda/en/latest/index.html)

```

```







