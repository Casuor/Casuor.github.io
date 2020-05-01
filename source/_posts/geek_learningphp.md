---
title: PHP Notes
categories: Geek
photos: https://cdn.jsdelivr.net/gh/Casuor/CDN@latest/Posts/Image/Common/xiangxiang.jpg
date: 2019-4-25
---
# PHP学习笔记

## 配置ApacheServer

PS::alarm_clock:IDE好用.

### 安装apache服务


    httpd -k install -n "Apache Server"


![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/Images20190916153446.png)

> 注：设置下面servername 即可，但一般使用虚拟主机，可以不对其设置

### 设置ServerName(可省略)

> F:\Develop_Apache_HttpServer\httpd-2.4.39-win64-VC15\Apache24\conf\httpd.conf

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/Images20190916153815.png)


    227 #ServerName www.example.com:80
    228 #ServerName localhost --设置


### 设置监听端口


    listen 80


每次更改重启服务

本机：localhost:80

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/Images/.Net%E5%BC%80%E5%8F%91Listen%20port.png)

### cmd进入Apache目录测试配置是否有错误


    httpd -t //测试配置是否OK


### 网站根目录

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/Images/.Net%E5%BC%80%E5%8F%91Root.png)


    DocumentRoot "${SRVROOT}/htdocs"
    <Directory "${SRVROOT}/htdocs">
    修改htdocs即可


更改后出现forbidden


    <Directory "${SRVROOT}/htdocs">#记得更改这个路径,一改全改
        #
        # Possible values for the Options directive are "None", "All",
        # or any combination of:
        #   Indexes Includes FollowSymLinks SymLinksifOwnerMatch ExecCGI MultiViews
        #
        # Note that "MultiViews" must be named *explicitly* --- "Options All"
        # doesn't give it to you.
        #
        # The Options directive is both complicated and important.  Please see
        # http://httpd.apache.org/docs/2.4/mod/core.html#options
        # for more information.
        #
        Options Indexes FollowSymLinks
        #
        # AllowOverride controls what directives may be placed in .htaccess files.
        # It can be "All", "None", or any combination of the keywords:
        #   AllowOverride FileInfo AuthConfig Limit
        #
        AllowOverride None
        #
        # Controls who can get stuff from this server.
        #
        Require all granted
    </Directory>


### 默认打开文档


    <IfModule dir_module>
        DirectoryIndex index.html
    </IfModule>



### 配置能否浏览目录结构


    <Directory "${SRVROOT}/htdocs">
        #
        # Possible values for the Options directive are "None", "All",
        # or any combination of:
        #   Indexes Includes FollowSymLinks SymLinksifOwnerMatch ExecCGI MultiViews
        #
        # Note that "MultiViews" must be named *explicitly* --- "Options All"
        # doesn't give it to you.
        #
        # The Options directive is both complicated and important.  Please see
        # http://httpd.apache.org/docs/2.4/mod/core.html#options
        # for more information.
        #
        Options Indexes FollowSymLinks		#看这里，去掉Indexes就访问不到了
        #
        # AllowOverride controls what directives may be placed in .htaccess  files.
        # It can be "All", "None", or any combination of the keywords:
        #   AllowOverride FileInfo AuthConfig Limit
        #
        AllowOverride None
        #
        # Controls who can get stuff from this server.
        #
        Require all granted
    </Directory>


### 配置虚拟主机(一台机器，多个网站)

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/Images/.Net%E5%BC%80%E5%8F%91%E8%99%9A%E6%8B%9F%E4%B8%BB%E6%9C%BA.png)

第一步

```
#行号		内容

510		# Virtual hosts
		#去除注释
511		Include conf/extra/httpd-vhosts.conf

```

第二步

> 本机目录：F:\Develop_Apache_HttpServer\httpd-2.4.39-win64-VC15\Apache24\conf\extra\httpd-vhosts.conf

```
注：	特意的要去host文件去设置域名
	 htdocs在这里即是根目录与config文件中要相同
	 由于多个虚拟主机一同工作，所以需设置域名
	 #*:80 监听绑定在当前电脑上的任意IP的80端口
<VirtualHost *:80>
#根目录
    DocumentRoot "${SRVROOT}/htdocs"
#域名，需要在C盘hosts文件(C:\Windows\System32\drivers\etc\hosts)去设置本机为此域名(127.0.0.1 apache.store)
    ServerName apache.store
#显示错误反馈邮箱，暂时用不到 
   #ServerAdmin webmaster@dummy-host2.example.com
#错误日志
    ErrorLog "logs/apache.store-error.log"
#日志
    CustomLog "logs/apache.store-access.log" common
</VirtualHost>
这个虚拟主机配置是默认配置。
测试：apache.store
```



### 请求响应流程

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/Images/.Net%E5%BC%80%E5%8F%9120190701211704.png)

### 让Apache支持PHP（解压PHP，加载模块，addtype ）

配置主配置文件

把apache的工作交给php做（apache雇佣php工作）

**配置前浏览器原样输出**

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/Images20190825102120.png)

**配置内容**

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/Images20190825102250.png)

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/Images20190825102424.png)

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/Images20190825102532.png)

配置完成

重启服务测试效果如图

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/GIRLS20191106144249.png)

### apache与PHP的关系

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/Images20190827105236.png)

## PHP基础

### PHP简介

PHP:Hypertext Preprocessor

https://www.php.net/manual/zh/history.php.php

### PHP开发工具

**PHP Storm**

配置:

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/GIRLS20191106144501.png)

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/GIRLS20191106144730.png)

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/GIRLS20191106152610.png)

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/GIRLS20191106153937.png)

出现图二的情况:

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/GIRLS20191106154232.png)

### PHP语法基础

#### PHP代码块及注释

```php
<?php
//此处是PHP代码
?>
/*
当是纯的PHP代码时，可省略闭合的"?>"
*/
#单行注释
```

#### PHP大小写敏感问题(变量)

1.PHP自定义函数，类和关键字（如echo ,if else）**不关心**大小写。

2.变量（存储信息的容器）大小写敏感。

> 变量规则：
>
> 变量以$符号开头，其后是变量的名称
>
> 变量名称必须以字母或下划线开头
>
> 变量名称不能以数字开头
>
> 变量名称只能包含字母数字字符和下划线（a-z,0-9以及_）
>
> 变量名称对大小写敏感（$y和$Y是两个不同的变量）

**注：**

变量在赋值时创建，创建输出文本需加双引号。

**变量的作用域:**

local（局部）
global（全局）
static（静态）

> 函数之外声明的变量拥有 Global 作用域，只能在函数以外进行访问。
>
> 函数内部声明的变量拥有 LOCAL 作用域，只能在函数内部进行访问。

```php
<?php
$x=5; // 全局作用域

function myTest() {
  $y=10; // 局部作用域
  echo "<p>测试函数内部的变量：</p>";
  echo "变量 x 是：$x";
  echo "<br>";
  echo "变量 y 是：$x";
} 

myTest();

echo "<p>测试函数之外的变量：</p>";
echo "变量 x 是：$x";
echo "<br>";
echo "变量 y 是：$x";
?>
```

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/Images20190928144831.png)

**PHP global 关键词**
global 关键词用于访问函数内的全局变量。

```php
<?php
$x=5;
$y=10;

function myTest() {
  global $x,$y;
  $y=$x+$y;
}

myTest();
echo $y; // 输出 15
?>
```

PHP 同时在名为 $GLOBALS[index] 的数组中存储了所有的全局变量。下标存有变量名。这个数组在函
数内也可以访问，并能够用于直接更新全局变量。

上面的例子可以这样重写：

```php
<?php
$x=5;
$y=10;

function myTest() {
  $GLOBALS['y']=$GLOBALS['x']+$GLOBALS['y'];
} 

myTest();
echo $y; // 输出 15
?>
```

#### PHP全局变量——超全局变量

PHP 中的许多预定义变量都是“超全局的”，这意味着它们在一个脚本的全部作用域中都可用。在函数或
方法中无需执行 global $variable; 就可以访问它们。

这些超全局变量是：

```
$GLOBALS 
$_SERVER 
$_REQUEST 
$_POST 
$_GET 
$_FILES 
$_ENV 
$_COOKIE 
$_SESSION
```

> $GLOBALS
>
> **用于在 PHP 脚本中的任意位置访问全局变量（从函数或方法中均可）。**
>
> **PHP 在名为 $GLOBALS[index] 的数组中存储了所有全局变量。变量的名字就是数组的键。**
>
> ```php
> <?php
> $x=75;
> $y=25;
> function addition(){
> 	$GLOBALS['variable'] = $GLOBALS['x'] +$GLOBALS['y'];
> }
> addition();
> echo "$variable";
> ?>
> ```
>
> $SERVER
>
> **保存关于报头、路径和脚本位置的信息。**
>
> 详见:PHP教程.pdf_P35
>
> ```php
> <?php
> echo $_SERVER['PHP_SELF'];
> echo "<br>";
> echo $_SERVER['HTTP_HOST'];
> echo "<br>";
> echo $_SERVER['SERVER_NAME'];
> echo "<br>";
> echo $_SERVER['HTTP_REFERER'];
> echo "<br>";
> echo $_SERVER['HTTP_USER_AGENT'];
> echo "<br>";
> echo $_SERVER['SCRIPT_NAME'];
> echo "<br>";
> 
> ```
>
> $REQUEST
>
> PHP $_REQUEST 用于收集 HTML 表单提交的数据。
>
> ```php
> //REQUEST用于获取html表单提交的数据
> <html>
> <head>
> </head>
> <body>
> <form action="<?php echo $_SERVER['PHP_SELF'];?>" method="post">
> Name: <input type="text" name="name">
> <input type="submit">
> </form>
> <?php
> $name = $_REQUEST['name'];
> echo $name;
> ?>
> </body>
> </html>
> 
> ```
>
> $POST
> PHP $_POST 广泛用于收集提交 method="post" 的 HTML 表单后的表单数据。$_POST 也常用于传递
> 变量。
>
> ```php
> PHP $_POST 广泛用于收集提交 method="post" 的 HTML 表单后的表单数据。$_POST 也常用于传递
> 变量。
> <html>
> <head>
> </head>
> <body>
> <form action="<?php echo $_SERVER['PHP_SELF'];?>" method="post">
> Name: <input type="text" name="name">
> <input type="submit">
> </form>
> <?php
> $name = $_POST['name'];
> echo $name;
> ?>
> </body>
> </html>
> ```
>
> $GET
>
> PHP $_GET 也可用于收集提交 HTML 表单 (method="get") 之后的表单数据。
>
> $_GET 也可以收集 URL 中的发送的数据。
>
> ```php
> <html>
> <body>
> <a href="$_GET.php?subject=php&web=www.w3cschool.com.cn">TEST $_GET</a><br>
> <?php
> echo 'study&nbsp;'.$_GET['subject'].'at&nbsp'.$_GET['web'];
> ?>
> </body>
> </html>
> ```
> $FILES
>
> `$_FILES` 主要用在当需要上传二进制文件的地方，录入上传一个abc.mp3文件，则服务器端需要获得该文件的相关信息，则通过变量 $_FILES 来取得。
> $_FILES 超级全局变量包含通过POST方法向服务器上传的数据的有关信息。这个超级全局变量与其他的变量有所不同，它是一个二维数组，包含5个元素。
>
> 注:
> ① 在 PHP 4.1.0 版本以前该数组的名称为 $HTTP_POST_FILES，它并不像 `$_FILES` 一样是自动全局变量。PHP 3 不支持 `$HTTP_POST_FILES` 数组。
> ② 如果表单中没有选择上传的文件，则 PHP 变量
>
> ```
>  $_FILES[‘userfile’][‘size’] 
> ```
>
> _的值将为 0，
>
> ```
> $_FILES[‘userfile’][‘tmp_name’] 
> ```
>
> 将为 none。
> ③ error字段5个错误码：
>
> UPLOAD_ERR_OK 文件成功上传
> UPLOAD_ERR_INI_SIZE 文件大小超出了
> MAX_FILE_SIZE 指令所指定的最大值。
> UPLOAD_ERR_FORM_SIZE 文件大小超出了MAX_FILE_SIZE 隐藏表单域参数（可选）指定的最大值。
> UPLOAD_ERR_PARTIAL 文件只上传了一部分UPLOAD_ERR_NO_FILE 上传表单中没有指定文件
>
> ![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/Images20190930214200.png)
>
> ``` php
> <html>
> <body>
> <form action="$_FILES.php" method="post" enctype="multipart/form-data">
> <input type="file" name="file" >
> <input type="submit" name="submit" value="上传">
> </form>
> <?php
> echo $_FILES['file']['name'];
> ?>
> </body>
> </html>
> ```
>
> $ENV
>
> PHP中的$_ENV是一个包含服务器端环境变量的数组，不同系统不完全一样。
> 部分变量示例：
> $_ENV[ ‘HOSTNAME’ ] 服务器的主机名
> $_ENV[ ‘SHELL’ ] 系统 shell
>
> $_ENV只是被动的接受服务器端的环境变量并把它们转换为数组元素，你可以尝试直接输出它：
>
> ```php
> <?php
> //输出内容格式清晰，ThinkPHP可以直接用dump()
> var_dump($_ENV);
> echo "<hr>";
> //输出到屏幕
> print_r($_ENV);
> echo "<hr>";
> //输出key-value键值对
> foreach($_ENV as $key=>$val){echo $key.'--------'.$val.'<br>';}
> ```
>
> $_COOKIE
>
> cookie 常用于识别用户。cookie 是服务器留在用户计算机中的小文件。每当相同的计算机通过浏览器请求页面时，它同时会发送 cookie。通过 PHP，您能够创建并取回 cookie 的值。
>
> ```php
> <html>
> <body>
> 
> <?php
> setcookie("user", "Alex Porter", 3600);
>  echo $_COOKIE['user'];
> ?>
> </body>
> </html>
> 
> ```
>
> $_SESSION
>
> PHP session 变量用于存储有关用户会话的信息，或更改用户会话的设置。Session 变量保存的信息是单一用户的，并且可供应用程序中的所有页面使用。
>
> 当您运行一个应用程序时，您会打开它，做些更改，然后关闭它。这很像一次会话。计算机清楚你是谁。它知道你何时启动应用程序，并在何时终止。但是在因特网上，存在一个问题：服务器不知道你是谁以及你做什么，这是由于 HTTP 地址不能维持状态。
> 通过在服务器上存储用户信息以便随后使用，PHP session 解决了这个问题（比如用户名称、购买商品等）。不过，会话信息是临时的，在用户离开网站后将被删除。如果您需要永久储存信息，可以把数据存储在数据库中。
> Session 的工作机制是：为每个访问者创建一个唯一的 id (UID)，并基于这个 UID 来存储变量。UID 存储在 cookie 中，亦或通过 URL 进行传导。
>
> ```php
> 
> <html>
> <body>
> <?php
> //①开始 PHP Session :
> //在您把用户信息存储到 PHP session 中之前，首先必须启动会话。
> //注释：session_start() 函数必须位于 标签之前
> 
> //session_start();
> 
> //②存储 和使用Session 变量：
> $_SESSION['views']=1;
> echo "views=". $_SESSION['views'];
> 
> //③终结 Session
> //如果您希望删除某些 session 数据，可以使用 unset() 或 session_destroy() 函数。
> //通过 unset() 函数用于释放指定的 session 变量：
> unset($_SESSION['views']);
> //通过 session_destroy() 函数彻底终结 session：
> //session_destroy();
> ?>
> </body>
> </html>
> ```
>
> 

#### **PHP魔术变量**

PHP 向它运行的任何脚本提供了大量的预定义常量。

不过很多常量都是由不同的扩展库定义的，只有在加载了这些扩展库时才会出现，或者动态加载后，或
者在编译时已经包括进去了。

有八个魔术常量它们的值随着它们在代码中的位置改变而改变。



>`__LINE__`
>
>```php
><?php
>echo "<br>";
>echo "这是第".__LINE__."行！";
>```
>

> `_FILE_`
>
> ```
> <!--文件的完整路径和文件名。如果用在被包含文件中，则返回被包含的文件名
> 自 PHP 4.0.2 起，__FILE__
> 总是包含一个绝对路径（如果是符号连接，则是解析后的绝对路径），
> 而在此之前的版本有时会包含一个相对路径。-->
> <?php
> echo '此文件位置在'.__FILE__.'.';
> ```

> `_DIr_`
>
> ```
> <!--__DIR__
> 文件所在的目录。如果用在被包括文件中，则返回被包括的文件所在的目录。
> 它等价于 dirname(__FILE__)。除非是根目录，否则目录中名不包括末尾的斜杠。
> (PHP 5.3.0中新 增)-->
> <?php
> echo '该文件位于 “ '  . __DIR__ . ' ” ';
> ```

> `_FUNCTION_`
>
> ```
> <!--
> __FUNCTION__函数名称（PHP 4.3.0 新加）。
> 自 PHP 5 起本常量返回该函数被定义时的名字（区分大小写）。
> 在 PHP 4 中该值总是小写字母的。
> -->
> <?php
> function test(){
> echo '方法名是'.__FUNCTION__;
> }
> test();
> ```

> `_CLASS_`
>
> ```
> <!--
> 类的名称（PHP 4.3.0 新加）。自 PHP 5 起本常量返回该类被定义时的名字（区分大小写）。
> 在 PHP 4 中该值总是小写字母的。类名包括其被声明的作用区域（例如 Foo\Bar）。注意自 PHP 5.4 起 __CLASS__ 对 trait 也起作用。
> 当用在 trait 方法中时，__CLASS__ 是调用 trait 方法的类的名字。
> -->
> <?php
> 
> class test
> {
>     function _print()
>     {
>         echo '类名为：' . __CLASS__ . "<br>";
>         echo '函数名为：' . __FUNCTION__;
>     }
> }
> $t = new test();
> $t->_print();
> ?>
> 
> 
> ```

> `__TRAIT__`
>
> ```
> <!--__TRAIT__
> Trait 的名字（PHP 5.4.0 新加）。自 PHP 5.4.0 起，PHP 实现了代码复用的一个方法，称为 traits。
> Trait 名包括其被声明的作用区域（例如 Foo\Bar）。
> 从基类继承的成员被插入的 SayWorld Trait 中的 MyHelloWorld 方法所覆盖。其行为 MyHelloWorld 类 中定义的方法一致。优先顺序是当前类中的方法会覆盖 trait 方法，而 trait 方法又覆盖了基类中的方 法。
> -->
> <?php
> class Base{
>     public function sayhello(){
>         echo "hello";
>     }
> }
> trait SayWorld{
>     public function sayhello(){
>         parent::sayhello();
>         echo "world";
>     }
> }
> class Myhelloworld extends Base{
>     use SayWorld;
> }
> $o=new Myhelloworld();
> $o->sayhello();
> ```

> `__METHOD__`
>
> ```
> <!--
> 返回该方法被定义时的名字（区分大小写）。
> -->
> <?php
> function test(){
>     echo '函数名为:'.__METHOD__;
> }
> test();
> 
> ```

> `_NAMESPACE_`
>
> ```
> <?php namespace MyProject;
> echo '命名空间为："', __NAMESPACE__, '"'; // 输出 "MyProject" \
> ?>
> 
> ```

#### PHP命名空间

PHP 命名空间可以解决以下两类问题：

1. 用户编写的代码与PHP内部的类/函数/常量或第三方类/函数/常量之间的名字冲突。 
2. 为很长的标识符名称(通常是为了缓解第一类问题而定义的)创建一个别名（或简短）的名称，提高 源代码的可读性

**定义命名空间**

默认情况下，所有常量、类和函数名都放在全局空间下，就和PHP支持命名空间之前一样。
命名空间通过关键字namespace 来声明。如果一个文件中包含命名空间，它必须在其它所有代码之前 声明命名空间。语法格式如下:

```
< ?php  // 定义代码在 'MyProject' 命名空间中  namespace MyProject;  
 
// ... 代码 ...  
```

你也可以在同一个文件中定义不同的命名空间代码，如：

```
< ?php  namespace MyProject1;  // MyProject1 命名空间中的PHP代码  
 
namespace MyProject2;  // MyProject2 命名空间中的PHP代码    
 
// 另一种语法 namespace MyProject3 { 
// MyProject3 命名空间中的PHP代码  
	}  
?>  
```

ps:不建议使用这种语法在单个文件中定义多个命名空间。建议使用下面的大括号形式的语法。

```php
<?php
namespace MyProject {
    const CONNECT_OK = 1;
    class Connection { /* ... */ }
    function connect() { /* ... */  }
}

namespace AnotherProject {
    const CONNECT_OK = 1;
    class Connection { /* ... */ }
    function connect() { /* ... */  }
}
?>
```

将全局的非命名空间中的代码与命名空间中的代码组合在一起，只能使用大括号形式的语法。全局代码必须用一个不带名称的 namespace 语句加上大括号括起来，例如：

```php
<?php
namespace MyProject {

const CONNECT_OK = 1;
class Connection { /* ... */ }
function connect() { /* ... */  }
}

namespace { // 全局代码
session_start();
$a = MyProject\connect();
echo MyProject\Connection::start();
}
?>
```

在声明命名空间之前唯一合法的代码是用于定义源文件编码方式的 declare 语句。所有非 PHP 代码包 括空白符都不能出现在命名空间的声明之前.

```php
<?php declare(encoding='UTF-8'); //定义多个命名空间和不包含在命名空间中的代码
namespace MyProject {
    const CONNECT_OK = 1;
    class Connection
    { /* ... */
    }

    function connect()
    { /* ... */
    }
}

namespace {
    session_start();
    $a = MyProject\connect();
    echo MyProject\connect()::start();
}
?>
<!--
F:\Develop_PHP\php-7.1.31-Win32-VC14-x64\php.exe F:\Develop_Apache_HttpServer\httpd-2.4.39-win64-VC15\Apache24\htdocs\PHP_Projects\PrimarySyntax\NameSpace\NameSpace.php
PHP Warning:  declare(encoding=...) ignored because Zend multibyte feature is turned off by settings in F:\Develop_Apache_HttpServer\httpd-2.4.39-win64-VC15\Apache24\htdocs\PHP_Projects\PrimarySyntax\NameSpace\NameSpace.php on line 1
PHP Fatal error:  Uncaught Error: Class name must be a valid object or a string in F:\Develop_Apache_HttpServer\httpd-2.4.39-win64-VC15\Apache24\htdocs\PHP_Projects\PrimarySyntax\NameSpace\NameSpace.php:16
Stack trace:
#0 {main}
  thrown in F:\Develop_Apache_HttpServer\httpd-2.4.39-win64-VC15\Apache24\htdocs\PHP_Projects\PrimarySyntax\NameSpace\NameSpace.php on line 16

Process finished with exit code 255
-->

```

**子命名空间**

与目录和文件的关系很象，PHP 命名空间也允许指定层次化的命名空间的名称。因此，命名空间的名 字可以使用分层次的方式定义:

```php+HTML
<?php
namespace MyProject\Sub\Level;
//声明分层次的单个命名空间
const CONNECT_OK = 1;
class Connection
{ /* ... */
}

function Connect()
{ /* ... */
}

?>
```

上面的例子创建了

常量 MyProject\Sub\Level\CONNECT_OK，

类 MyProject\Sub\Level\Connection

函数 MyProject\Sub\Level\Connection。

**命名空间使用**

> PHP 命名空间中的类名可以通过三种方式引用：
>
> 1. **非限定名称，或不包含前缀的类名称，**例如 $a=new foo(); 或 foo::staticmethod();。如果当前命名空间是 currentnamespace，foo 将被解析为 currentnamespace\foo。如果使用 foo 的代码是全局的，不包含在任何命名空间中的代码，则 foo 会被解析为foo。 
>
>    PS：如果命名空间中的函数或常量未定义，则该非限定的函数名称或常量名称会被解析为全局函数名称或常量名称。
>
> 2. **限定名称,或包含前缀的名称，**例如 $a = new subnamespace\foo(); 或 subnamespace\foo::staticmethod();。如果当前的命名空间是 currentnamespace，则 foo 会被解析为 currentnamespace\subnamespace\foo。如果使用 foo 的代码是全局的，不包含在任何命名空间中的代码，foo 会被解析为subnamespace\foo。
>
> 3. **完全限定名称，或包含了全局前缀操作符的名称，**例如， $a = new \currentnamespace\foo(); 或 \currentnamespace\foo::staticmethod();。在这种情况下，foo 总是被解析为代码中的文字名(literal name)currentnamespace\foo。

DEMO01

```php
<?php
namespace Foo\Bar\Subnamespace;

const FOO=1;
function foo(){}
class foo{
    static  function staticmethod(){}
}
?>
```

DEMO02

```php
<?php
namespace Foo\Bar;//命名空间为Foo\Bar,位于Foo下
include "Demo01NameSpace.php";

//echo "全局代码应包含在全局名称空间声明中";

const FOO=2;
function Foo(){}
class Foo{
    static function staticmethod(){}
}
/* 非限定名称 */
foo();
// 解析为 Foo\Bar\foo这个函数
foo::staticmethod();
// 解析为类 Foo\Bar\foo的静态方法staticmethod。
echo FOO;
// 解析为 Foo\Bar\ FOO这个常量



/* 限定名称 */
subnamespace\foo();
// 解析为函数 Foo\Bar\subnamespace\foo
subnamespace\foo::staticmethod();
// 解析为类 Foo\Bar\subnamespace\foo,
// 以及类的方法 staticmethod

echo subnamespace\FOO;
/// 解析为常量 Foo\Bar\subnamespace\FOO



/* 完全限定名称 */
\Foo\Bar\foo();
// 解析为函数 Foo\Bar\foo
\Foo\Bar\foo::staticmethod();
// 解析为类 Foo\Bar\foo, 以及类的方法 staticmethod
echo \Foo\Bar\FOO;
// 解析为常量 Foo\Bar\FOO
```

DEMO03

```php
<?php
namespace Foo;//命名空间为Foo
function strlen() {}
const INI_ALL = 3;
class Exception {}

$a = \strlen('hi'); // 调用全局函数strlen
$b = \INI_ALL; // 访问全局常量 INI_ALL
$c = new \Exception('error'); // 实例化全局类 Exception
```

:orange: PS:不就是路径访问的结构,具体怎么实现不知道

**命名空间和动态语言特征**

PHP 命名空间的实现受到其语言自身的动态特征的影响。因此，如果要将下面的代码转换到命名空间中，动态访问元素。

DEMO01

```php
<?php
class cname{
    function __construct()
    {
        echo __METHOD__,"\n";//输出方法名:__construct
    }
}
function fname(){
    echo __FUNCTION__,"\n";//输出方法名:fname
}
const conname="global";//常量:conname

$a='cname';
$obj = new $a;//打印cname::__construct
$b='fname';
$b(); //打印fname
echo constant('conname'),"\n";//打印conname
```

输出结果:

```
cname::__construct fname global 
//嗯结果打印了全局的结构类,方法,常量
```

必须使用完全限定名称（包括命名空间前缀的类名称）。注意因为在动态的类名称、函数名称或常量名称中，限定名称和完全限定名称没有区别，因此其前导的反斜杠是不必要的。

动态访问命名空间的元素

DEMO02

```php
<?php
namespace namespacename;
class cname
{
    function __construct()
    {
        echo __METHOD__,"\n";
    }
}
function fname()
{
    echo __FUNCTION__,"\n";
}
const constname = "global";

include 'Demo04NameSpace&Dynamic.php';

$a = 'cname';
$obj = new $a; // prints classname::__construct
$b = 'fname';
$b(); // prints funcname
echo constant('constname'), "\n"; // prints global
//echo constant("namespacename\constname"),"\n";
/* note that if using double quotes, "\\namespacename\\classname" must be used */
$a = '\namespacename\cname';
$obj = new $a; // prints namespacename\classname::__construct
$a = 'namespacename\cname';
$obj = new $a; // also prints namespacename\classname::__construct
$b = 'namespacename\fname';
$b(); // prints namespacename\funcname
$b = '\namespacename\fname';
$b(); // also prints namespacename\funcname
echo constant('\namespacename\constname'), "\n"; // prints namespaced
echo constant('namespacename\constname'), "\n"; // also prints namespaced
?>
```

输出结果:

```
error:Couldn't find constant constname
```

:orange: PS:这这讲的不是一个问题吗

**`namespace`关键字和`__NAMESPACE__`常量**



#### PHP static 关键词

通常，当函数完成/执行后，会删除所有变量。不过，有时我需要不删除某个局部变量。实现这一点需
要首次声明变量时使用 static 关键词。

```php
<?php

function myTest() {
  static $x=0;


  echo $x;
  $x++;
}

myTest();
myTest();
myTest();

?>
```

然后，每当函数被调用时，这个变量所存储的信息都是函数最后一次被调用时所包含的信息。

注释：该变量仍然是函数的局部变量。

#### PHP数据类型

PHP是一种松散型语言，不用告知类型，自动数据类型。

**字符串、整数、浮点数、逻辑、数组、对象、NULL。**

> 字符串可以是引号内的任何文本。您可以使用单引号或双引号。
>
> 
>
> 整数是没有小数的数字。
>
> 整数规则：
>
> 整数必须有至少一个数字（0-9）
> 整数不能包含逗号或空格
> 整数不能有小数点
> 整数正负均可
> 可以用三种格式规定整数：十进制、十六进制（前缀是 0x）或八进制（前缀是 0）
>
> **PHP var_dump() 会返回变量的数据类型和值。**
>
> ```php
> <?php
> $x=5985;
> var_dump($x);
> echo("<br>");
> 
> $x=-345;
> var_dump($x);
> echo("<br>");
> 
> $x=0x8C;
> var_dump($x);
> echo("<br>");
> 
> $x=047;
> var_dump($x);
> echo("<br>");
> ?>
> 
> 结果：
> int(5985)
> int(-345)
> int(140)
> int(39)
> ```
>
> 
>
> 浮点数是有小数点或指数形式的数字。
>
> ```php
> <?php
> $x=10.365;
> var_dump($x);
> echo("<br>");
> 
> $x=2.4e3;
> var_dump($x);
> echo("<br>");
> 
> $x=8E-5;
> var_dump($x);
> echo("<br>");
> ?>
> 结果：    
> float(10.365)
> float(2400)
> float(8.0E-5)
> ```
>
> 
>
> 逻辑是 true 或 false。
>
> 
>
> **数组**在一个变量中存储多个值。
>
> ```php
> <?php
> $cars=array("volvo","bwm","saab");
> var_dump($cars);
> ?>
> 结果：
> array(3) { [0]=> string(5) "volvo" [1]=> string(3) "bwm" [2]=> string(4) "saab" }
> ```
>
> **创建数组**
>
> 在 PHP 中， array() 函数用于创建数组：
>
> ```php
> array();
> ```
>
> **在 PHP 中，有三种数组类型：**
>
> **索引数组 - 带有数字索引的数组**
>
> 有两种创建索引数组的方法：
>
> 索引是自动分配的（索引从 0 开始）：
>
> ```php
> $cars=array("Volvo","BMW","SAAB");
> ```
>
> 手动分配索引
>
> ```php
> $cars[0]="Volvo";
> $cars[1]="BMW";
> $cars[2]="SAAB";
> ```
>
> **关联数组 - 带有指定键的数组**
>
> 关联数组是使用您分配给数组的指定键的数组。
>
> 有两种创建关联数组的方法：
>
> ```php
> $age=array("Peter"=>"35","Ben"=>"37","Joe"=>"43");
> ```
>
> ```php
> $age['Peter']="35";
> $age['Ben']="37";
> $age['Joe']="43";
> ```
>
> **多维数组 - 包含一个或多个数组的数组**
>
> **数组的方法**
>
> **获得数组的长度 - count() 函数**
>
> ```php
> <?php
> $cars=array("Volvo","BMW","SAAB");
> echo count($cars);
> ?>
> ```
>
> **PHP - 数组的排序函数**
>
> sort() - 以升序对数组排序
> rsort() - 以降序对数组排序
> asort() - 根据值，以升序对关联数组进行排序
> ksort() - 根据键，以升序对关联数组进行排序
> arsort() - 根据值，以降序对关联数组进行排序
> krsort() - 根据键，以降序对关联数组进行排序
>
> **遍历一般数组**
>
> ```php
><?php
> $cars = array('volvo' ,'bmw','saab' );
> $arraylenth=count($cars);
> for ($i=0; $i <$arraylenth ; $i++) { 
> 	echo $cars[$i];
> 	echo "<br>";
> }
> ?>
> ```
> 
> **遍历关联数组**
>
> ```php
><?php
> $age=array("Bill"=>"35","Steve"=>"37","Peter"=>"43");
> 
> foreach($age as $x=>$x_value) {
> echo "Key=" . $x . ", Value=" . $x_value;
> echo "<br>";
> }
> ?>
> ```
> 
> 
>
> 对象是存储数据和有关如何处理数据的信息的数据类型。
>
> 在 PHP 中，必须明确地声明对象。
>
> 首先我们必须声明对象的类。对此，我们使用 class 关键词。类是包含属性和方法的结构。
>
> 然后我们在对象类中定义数据类型，然后在该类的实例中使用此数据类型：
>
> ```php
><?php
> class car{
> 	var $color;
> 	function car($color="green"){
> 		$this->color=$color;
> 	}
> 	function what_color(){
> 		return $this->color;
> 	}
> 
> }
> ?>
> ```
> 
> 
>
> 特殊的 NULL 值表示变量无值。NULL 是数据类型 NULL 唯一可能的值。
>
> NULL 值标示变量是否为空。也用于区分空字符串与空值数据库。
>
> 可以通过把值设置为 NULL，将变量清空：

#### PHP的输出方法

> echo 和 print 之间的差异：
>
> echo - 能够输出一个以上的字符串
> print - 只能输出一个字符串，并始终返回 1
>
> 提示：echo 比 print 稍快，因为它不返回任何值。
>
> echo 是一个语言结构，有无括号均可使用：echo 或 echo()。
>
> print 也是语言结构，有无括号均可使用：print 或 print()。

**显示字符串**

```php
<?php
echo "<h2>PHP is fun!</h2>";
echo "Hello world!<br>";
echo "I'm about to learn PHP!<br>";
echo "This", " string", " was", " made", " with multiple parameters.";
?>
```

```php+HTML
<?php
print "<h2>PHP is fun!</h2>";
print "Hello world!<br>";
print "I'm about to learn PHP!";
?>
```

**显示变量**

```php
<?php
$txt1="learn php";
$txt2="w3school.com.cn";
$cars=array("volvo","bwm","saab");

echo $txt1;
echo "<br>";
echo "study php at $txt2";
echo "<br>";
echo "my car is a {$cars[0]}";
?>
```

#### PHP常用函数

**字符串函数**

strlen()字符串长度

```php
<?php
echo strlen("hello world");
?>
```

strpos() 函数用于检索字符串内指定的字符或文本。

如果找到匹配，则会返回首个匹配的字符位置。如果未找到匹配，则将返回 FALSE。

```php
<?php
echo strpos("hello world", "world");
?>
结果：6
```

#### PHP 常量

> 常量是单个值的标识符（名称）。在脚本中无法改变该值。
>
> 有效的常量名以字符或下划线开头（常量名称前面没有 $ 符号）。
>
> 注释：与变量不同，常量贯穿整个脚本是自动全局的。
>
> **设置 PHP 常量**
> 如需设置常量，请使用 define() 函数 - 它使用三个参数：
>
>
> 1. 首个参数定义常量的名称
> 2. 第二个参数定义常量的值
> 3. 可选的第三个参数规定常量名是否对大小写敏感。默认是 false。
>
> ```php
> <?php
> define('greeting', 'welcome to w3cschool.com.cn');
> echo(greeting);
> ?>
> ```
>
> ```php
> <?php
> define('greeting', 'welcome to w3cschool.com.cn',true);
> echo(GREETING);
> ?>
> ```

#### PHP运算符

> PHP 算数运算符——+-*/%

> PHP 赋值运算符——略

> PHP 字符串运算符
>
> . 串接 
>
> .= 串接赋值
>
> ```php
> <?php
> $a="hello";
> $b=$a."  world!";
> echo($b."<br>");
> $a.="world!!!";
> echo($a);
> ?>
> ```

> PHP 递增/递减运算符
>
> ++$x 	前递增 	$x 加一递增，然后返回 $x
> $x++ 	后递增	 返回 $x，然后 $x 加一递增
> --$x 	  前递减 	$x 减一递减，然后返回 $x
> $x-- 	  后递减 	返回 $x，然后 $x 减一递减
>
> ```php
> <?php
> $x=10; 
> echo ++$x; // 输出 11
> 
> 
> $y=10; 
> echo $y++; // 输出 10
> 
> $z=5;
> echo --$z; // 输出 4
> 
> $i=5;
> echo $i--; // 输出 5
> ?>
> ```

> PHP 比较运算符
>
> ![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/Images20190929142916.png)
>
> ```php+HTML
> <?php
> $x=10; 
> 
> $y='10'; 
> 
> echo("==");
> var_dump($x==$y);
> echo("<br>"."===");
> var_dump($x===$y);
> ?>
> ```

> PHP 逻辑运算符
>
> ![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/Images20190929143249.png)

> PHP 数组运算符
>
> ![1569739478312](C:\Users\16877\AppData\Roaming\Typora\typora-user-images\1569739478312.png)
>
> ```php
> <?php
> $x = array('a' =>"red" ,"b"=>"green");
> $y = array('c' =>"blue" ,"d"=>"yellow");
> $a = array('a' => "orange", "f"=>"pink");
> $b = array('e' => "red", "f"=>"pink");
> $z=$x+$y;
> $c=$x+$a;
> $d=$x+$b;
> var_dump($z);
> echo("<br>");
> var_dump($c);
> echo("<br>");
> var_dump($d);
> echo("<br>");
> var_dump($x==$y);
> echo("<br>");
> var_dump($x===$y);
> echo("<br>");
> var_dump($x!=$y);
> echo("<br>");
> var_dump($x<>$y);
> echo("<br>");
> var_dump($x!==$y);
> ?>
>     结果：
> array(4) { ["a"]=> string(3) "red" ["b"]=> string(5) "green" ["c"]=> string(4) "blue" ["d"]=> string(6) "yellow" }
> array(3) { ["a"]=> string(3) "red" ["b"]=> string(5) "green" ["f"]=> string(4) "pink" }
> array(4) { ["a"]=> string(3) "red" ["b"]=> string(5) "green" ["e"]=> string(3) "red" ["f"]=> string(4) "pink" }
> bool(false)
> bool(false)
> bool(true)
> bool(true)
> bool(true)
> ```

#### PHP 条件语句

> PHP if else 语句

> PHP Switch 语句
>
> 语法
>
> ```php
> switch (expression)
> {
> case label1:
>   code to be executed if expression = label1;
>   break;  
> case label2:
>   code to be executed if expression = label2;
>   break;
> default:
>   code to be executed
>   if expression is different 
>   from both label1 and label2;
> }
> ```
>
> 工作原理
>
> 1. 对表达式（通常是变量）进行一次计算
> 2. 把表达式的值与结构中 case 的值进行比较
> 3. 如果存在匹配，则执行与 case 关联的代码
> 4. 代码执行后，break 语句阻止代码跳入下一个 case 中继续执行
> 5. 如果没有 case 为真，则使用 default 语句

> PHP while 循环
>
> while - 只要指定条件为真，则循环代码块
> do...while - 先执行一次代码块，然后只要指定条件为真则重复循环
> for - 循环代码块指定次数
> foreach - 遍历数组中的每个元素并循环代码块
>
> 注：
>
> 语法
>
> ```php
> foreach ($array as $value) {
>   code to be executed;
> }
> ```
>
> 每进行一次循环迭代，当前数组元素的值就会被赋值给 $value 变量，并且数组指针会逐一地移动，直
> 到到达最后一个数组元素。
>
> ```php
> <?php
> $colors = array('red','green','blue','yellow' );
> foreach ($colors as  $value) {
> 	echo "$value<br>";
> }
> ?>
> ```

#### PHP函数

> 注:
>
> PHP 默认参数值
>
> 下面的例子展示了如何使用默认参数。如果我们调用没有参数的 setHeight() 函数，它的参数会取默认
> 值：
>
> ```php
> <?php
> function setHeight($mineheight=50){
>  echo "the height is:$mineheight<br>";
> } 
> 
> setHeight(350);
> setHeight();
> ?>
> ```



