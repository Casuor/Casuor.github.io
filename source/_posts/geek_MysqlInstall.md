---
title: Mysql install for windows
categories: Geek
photos: https://cdn.jsdelivr.net/gh/Casuor/CDN@latest/Posts/Image/Common/xiangxiang.jpg
date: 2018-4-25
---
# Mysql离线安装教程（5.7.26）

### 1.下载

[官网直达](https://dev.mysql.com/downloads/mysql/)

### 2.解压并创建my.ini文件


    [mysql]
    # 设置mysql客户端默认字符集
    default-character-set=utf8 
    [mysqld]
    # 设置3306端口
    port = 3306 
    # 设置mysql的安装目录
    basedir=F:\Develop_MySQL\mysql-5.7.26-winx64	 #自己改
    # 设置mysql数据库的数据的存放目录
    datadir=F:\Develop_MySQL\mysql-5.7.26-winx64\data #自己改
    # 允许最大连接数
    max_connections=200
    # 设置mysql服务端默认字符集
    character-set-server=utf8


### 3.配置环境变量（可省略）

path中添加“F:\Develop_MySQL\mysql-5.7.26-winx64\bin”

此步骤省略需进入“F:\Develop_MySQL\mysql-5.7.26-winx64\bin”执行以下指令，反之。

### 4.初始化数据库

管理员运行cmd


    mysqld --initialize --user=mysql --console 


最后一行是**随机生成的密码**　

初始化时出现问题:


    TIMESTAMP with implicit DEFAULT value is deprecated. Please use --explicit_defaults_for_timestamp server option (see documentation for more details)


表明已经初始化过,建议删了重新弄

删除`mysql`


    HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\services\eventlog\Application\MySQL




### 5.安装`MySQL`服务


    mysqld --install


### 6.开启服务


    net start mysql


### 7.进入操作（不解释操作）


    mysql -u root -p


进入时密码一般为空或者生成的随机密码

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/Images

### 8.修改初始密码

方式一（命令行）

进入数据库，键入：


    ./mysqladmin -uroot -p password


方式二（管理工具Navicat）

### 9.软件链接

链接：https://pan.baidu.com/s/1vVOcs_Y2iW6HdM5m3irW0w 
提取码：h51w 

### 其他版本自行百度
