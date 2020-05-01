---
title: Flutter Notes
categories: Geek
photos: https://cdn.jsdelivr.net/gh/Casuor/CDN@latest/Posts/Image/Common/xiangxiang.jpg
date: 2019-8-25
---
# 起步
## 移动开发技术简介
### 跨平台技术简介
#### H5+原生（Cordova、Ionic、微信小程序）

​    动态内容通过H5实现(原生的网页加载控件webview,不难理解),APP相当于浏览器.这种模式称为混合应用,或Hybrid APP.
​    代表:微信小程序
​    混合开发技术:
​      webview实质上是一个浏览器内核,实现交互需要js,而对于js直接操纵系统(原生API)能力有限,即需要使用原生与H5混合的开发模式.
​      js与原生API之间通信遵守一个标准协议,协议实现的工具:webview javascipt bridge.
​      JavaScript开发+原生渲染的方式主要优点如下：

采用Web开发技术栈，社区庞大、上手快、开发成本相对较低。
原生渲染，性能相比H5提高很多。
动态化较好，支持热更新。

​		不足：

渲染时需要JavaScript和原生之间通信，在有些场景如拖动可能会因为通信频繁导致卡顿。
JavaScript为脚本语言，执行时需要JIT(Just In Time)，执行效率和AOT(Ahead Of Time)代码仍有差距。
由于渲染依赖原生控件，不同平台的控件需要单独维护，并且当系统更新时，社区控件可能会滞后；除此之外，其控件系统也会受到原生UI系统限制，例如，在Android中，手势冲突消歧规则是固定的，这在使用不同人写的控件嵌套时，手势冲突问题将会变得非常棘手。:Hybrid(杂种;混合物)

#### JavaScript开发+原生渲染 （React Native、Weex、快应用）

​    React Native简介
​    React Native (简称RN)是Facebook于2015年4月开源的跨平台移动应用开发框架，是Facebook早先开源的JS框架 React 在原生移动应用平台的衍生产物，目前支持iOS和Android两个平台。RN使用Javascript语言，类似于HTML的JSX，以及CSS来开发移动应用，因此熟悉Web前端开发的技术人员只需很少的学习就可以进入移动应用开发领域。
​    由于RN和React原理相通，并且Flutter也是受React启发，很多思想也都是相通的，万丈高楼平地起，我们有必要深入了解一下React原理。React是一个响应式的Web框架，我们先了解一下两个重要的概念：DOM树与响应式编程。
​        >DOM树:
​        >响应式编程:
​    PS:
​        >react?
​      -Weex简介
​          Weex是阿里巴巴于2016年发布的跨平台移动端开发框架，思想及原理和React Native类似，最大的不同是语法层面，Weex支持Vue语法和Rax语法，Rax 的 DSL(Domain Specific Language) 语法是基于 React JSX 语法而创造。与 React 不同，在 Rax 中 JSX 是必选的，它不支持通过其它方式创建组件，所以学习 JSX 是使用 Rax 的必要基础。而React Native只支持JSX语法。
​      -快应用简介
​          采用JavaScript语言开发，原生控件渲染，与React Native和Weex相比主要有两点不同：
​          快应用自身不支持Vue或React语法，其采用原生JavaScript开发，其开发框架和微信小程序很像，值得一提的是小程序目前已经可以使用Vue语法开发（mpvue），从原理上来讲，Vue的语法也可以移植到快应用上。
​          React Native和Weex的渲染/排版引擎是集成到框架中的，每一个APP都需要打包一份，安装包体积较大；而快应用渲染/排版引擎是集成到ROM中的，应用中无需打包，安装包体积小，正因如此，快应用才能在保证性能的同时做到快速分发。

#### 自绘UI+原生(QT for mobile、Flutter)

​    QT :
​    

## 初识Flutter

### Flutter简介

 Flutter 是 Google推出并开源的移动应用开发框架，主打跨平台、高保真、高性能。开发者可以通过 Dart语言开发 App，一套代码同时运行在 iOS 和 Android平台。 Flutter提供了丰富的组件、接口，开发者可以很快地为 Flutter添加 native扩展。同时 Flutter还使用 Native引擎渲染视图，这无疑能为用户提供良好的体验。 

#### 跨平台自绘引擎

Flutter与用于构建移动应用程序的其它大多数框架不同，因为Flutter既不使用WebView，也不使用操作系统的原生控件。 相反，Flutter使用自己的高性能渲染引擎来绘制widget。这样不仅可以保证在Android和iOS上UI的一致性，而且也可以避免对原生控件依赖而带来的限制及高昂的维护成本。

Flutter使用Skia作为其2D渲染引擎，Skia是Google的一个2D图形处理函数库，包含字型、坐标转换，以及点阵图都有高效能且简洁的表现，Skia是跨平台的，并提供了非常友好的API，目前Google Chrome浏览器和Android均采用Skia作为其绘图引擎。

目前Flutter目前默认支持iOS、Android、Fuchsia（Google新的自研操作系统）三个移动平台。但Flutter亦可支持Web开发（Flutter for web）和PC开发，本书的示例和介绍主要是基于iOS和Android平台的，其它平台读者可以自行了解。

#### 高性能

 Flutter高性能主要靠两点来保证，首先，Flutter APP采用Dart语言开发。Dart在 JIT（即时编译）模式下，速度与 JavaScript基本持平。但是 Dart支持 AOT，当以 AOT模式运行时，JavaScript便远远追不上了。速度的提升对高帧率下的视图数据计算很有帮助。其次，Flutter使用自己的渲染引擎来绘制UI，布局数据等由Dart语言直接控制，所以在布局过程中不需要像RN那样要在JavaScript和Native之间通信，这在一些滑动和拖动的场景下具有明显优势，因为在滑动和拖动过程往往都会引起布局发生变化，所以JavaScript需要和Native之间不停的同步布局信息，这和在浏览器中要JavaScript频繁操作DOM所带来的问题是相同的，都会带来比较可观的性能开销。 

#### 采用Dart语言开发

这是一个很有意思，但也很有争议的问题，在了解Flutter为什么选择了 Dart而不是 JavaScript之前我们先来介绍两个概念：JIT和AOT。

目前，程序主要有两种运行方式：`静态编译与动态解释。`

静态编译的程序在执行前全部被翻译为机器码，通常将这种类型称为**AOT** （Ahead of time）即 “提前编译”；

动态解释执行的则是一句一句边翻译边运行，通常将这种类型称为**JIT**（Just-in-time）即“即时编译”。

AOT程序的典型代表是用`C/C++`开发的应用，它们必须在执行前编译成机器码，而JIT的代表则非常多，如JavaScript、python等，**事实上，所有脚本语言都支持JIT模式**。但需要注意的是JIT和AOT指的是程序运行方式，和编程语言并非强关联的，有些语言既可以以JIT方式运行也可以以AOT方式运行，如Java、Python，它们可以在第一次执行时编译成中间字节码、然后在之后执行时可以直接执行字节码，也许有人会说，中间字节码并非机器码，在程序执行时仍然需要动态将字节码转为机器码，是的，这没有错，不过**通常我们区分是否为AOT的标准就是看代码在执行之前是否需要编译，只要需要编译，无论其编译产物是字节码还是机器码，都属于AOT。**

现在我们看看Flutter为什么选择Dart语言？笔者根据官方解释以及自己对Flutter的理解总结了以下几条（由于其它跨平台框架都将JavaScript作为其开发语言，所以主要将Dart和JavaScript做一个对比）：

1. **开发效率高**

   Dart运行时和编译器支持Flutter的两个关键特性的组合：

   **基于JIT的快速开发周期**：Flutter在开发阶段采用，采用JIT模式，这样就避免了每次改动都要进行编译，极大的节省了开发时间；

   **基于AOT的发布包**: Flutter在发布时可以通过AOT生成高效的ARM代码以保证应用性能。而JavaScript则不具有这个能力。 

2. **高性能**

Flutter旨在提供流畅、高保真的的UI体验。为了实现这一点，Flutter中需要能够在每个动画帧中运行大量的代码。这意味着需要一种既能提供高性能的语言，而不会出现会丢帧的周期性暂停，而Dart支持AOT，在这一点上可以做的比JavaScript更好。

3.**快速内存分配**

Flutter框架使用函数式流，这使得它在很大程度上依赖于底层的内存分配器。因此，拥有一个能够有效地处理琐碎任务的内存分配器将显得十分重要，在缺乏此功能的语言中，Flutter将无法有效地工作。当然Chrome V8的JavaScript引擎在内存分配上也已经做的很好，事实上Dart开发团队的很多成员都是来自Chrome团队的，所以在内存分配上Dart并不能作为超越JavaScript的优势，而对于Flutter来说，它需要这样的特性，而Dart也正好满足而已。

4.**类型安全**

由于Dart是类型安全的语言，支持静态类型检测，所以可以在编译前发现一些类型的错误，并排除潜在问题，这一点对于前端开发者来说可能会更具有吸引力。与之不同的，JavaScript是一个弱类型语言，也因此前端社区出现了很多给JavaScript代码添加静态类型检测的扩展语言和工具，如：微软的TypeScript以及Facebook的Flow。相比之下，Dart本身就支持静态类型，这是它的一个重要优势。

5.**Dart团队就在你身边**

看似不起眼，实则举足轻重。由于有Dart团队的积极投入，Flutter团队可以获得更多、更方便的支持，正如Flutter官网所述“我们正与Dart社区进行密切合作，以改进Dart在Flutter中的使用。例如，当我们最初采用Dart时，该语言并没有提供生成原生二进制文件的工具链（这对于实现可预测的高性能具有很大的帮助），但是现在它实现了，因为Dart团队专门为Flutter构建了它。同样，Dart VM之前已经针对吞吐量进行了优化，但团队现在正在优化VM的延迟时间，这对于Flutter的工作负载更为重要。”

### Flutter框架结构

![](https://cdn.jsdelivr.net/gh/flutterchina/flutter-in-action/docs/imgs/1-1.png)

#### Flutter Framework

这是一个纯 Dart实现的 SDK，它实现了一套基础库，自底向上，我们来简单介绍一下：

- 底下两层（Foundation和Animation、Painting、Gestures）在Google的一些视频中被合并为一个dart UI层，对应的是Flutter中的`dart:ui`包，它是Flutter引擎暴露的底层UI库，提供动画、手势及绘制能力。
- Rendering层，这一层是一个抽象的布局层，它依赖于dart UI层，Rendering层会构建一个UI树，当UI树有变化时，会计算出有变化的部分，然后更新UI树，最终将UI树绘制到屏幕上，这个过程类似于React中的虚拟DOM。Rendering层可以说是Flutter UI框架最核心的部分，它除了确定每个UI元素的位置、大小之外还要进行坐标变换、绘制(调用底层dart:ui)。
- Widgets层是Flutter提供的的一套基础组件库，在基础组件库之上，Flutter还提供了 Material 和Cupertino两种视觉风格的组件库。而**我们Flutter开发的大多数场景，只是和这两层打交道**。

#### Flutter Engine

这是一个纯 C++实现的 SDK，其中包括了 Skia引擎、Dart运行时、文字排版引擎等。在代码调用 `dart:ui`库时，调用最终会走到Engine层，然后实现真正的绘制逻辑。

### 学习Flutter

#### 资源

- **官网**：阅读Flutter官网的资源是快速入门的最佳方式，同时官网也是了解最新Flutter发展动态的地方，由于目前Flutter仍然处于快速发展阶段，所以建议读者还是时不时的去官网看看有没有新的动态。
- **源码及注释**：源码注释应作为学习Flutter的第一文档，Flutter SDK的源码是开源的，并且注释非常详细，也有很多示例，实际上，Flutter官方的SDK文档就是通过注释生成的。源码结合注释可以帮你解决大多数问题。
- **Github**：如果遇到的问题在StackOverflow上也没有找到答案，可以去github flutter 项目下提issue。
- `Gallery源码`：Gallery是Flutter官方示例APP，里面有丰富的示例，读者可以在网上下载安装。Gallery的源码在Flutter源码“examples”目录下。

##  搭建Flutter开发环境

#### 获取Flutter SDK

[FlutterSDK](https://flutter.dev/docs/get-started/install/windows)

#### Windows下安装

解压到任意盘:

用户变量:

Path:追加xxx/Flutter/Bin/

新建:

变量名=变量值

```
PUB_HOSTED_URL=https://pub.flutter-io.cn
```

```
FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
```

重启电脑

运行`flutter doctor -v`

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/GIRLS20191108212527.png)

逐步解决

1.安装插件

Flutter&Dart

2.配置环境变量

ANDROID_HOME=F:\Develop_AndroidStudio\AndroidSDK\platform-tools

Path下添加F:\Develop_AndroidStudio\AndroidSDK\platform-tools

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/GIRLS20191108214537.png)

Problem:Android license status Unknow.

Solution:[ https://www.wandouip.com/t5i325108/ ](https://www.wandouip.com/t5i325108/)

简要记录下:

F:\Develop_AndroidStudio\AndroidSDK\tools\bin目录下

执行:

```
sdkmanager.bat --update
```

出现错误:

```
Exception in thread "main" java.lang.NoClassDefFoundError: javax/xml/bind/annotation/XmlSchema
        at com.android.repository.api.SchemaModule$SchemaModuleVersion.<init>(SchemaModule.java:156)
        at com.android.repository.api.SchemaModule.<init>(SchemaModule.java:75)
        at com.android.sdklib.repository.AndroidSdkHandler.<clinit>(AndroidSdkHandler.java:81)
        at com.android.sdklib.tool.sdkmanager.SdkManagerCli.main(SdkManagerCli.java:73)
        at com.android.sdklib.tool.sdkmanager.SdkManagerCli.main(SdkManagerCli.java:48)
Caused by: java.lang.ClassNotFoundException: javax.xml.bind.annotation.XmlSchema
        at java.base/jdk.internal.loader.BuiltinClassLoader.loadClass(BuiltinClassLoader.java:583)
        at java.base/jdk.internal.loader.ClassLoaders$AppClassLoader.loadClass(ClassLoaders.java:178)
        at java.base/java.lang.ClassLoader.loadClass(ClassLoader.java:521)
        ... 5 more
```

根据笔者的解决方法:(原因是java版本8就可以java9之后阉割了一些库,本人`12.0.2`)

需要添加jaxb相关依赖： 

下载:

:jack_o_lantern: activation.jar
:jack_o_lantern: jaxb-api.jar
:jack_o_lantern: jaxb-core.jar
:jack_o_lantern: jaxb-impl.jar
:jack_o_lantern: jaxb-jxc.jar
:jack_o_lantern: jaxb-xjc.jar

jar地址:

[java2s](http://www.java2s.com/)

[jar-download](https://jar-download.com/)

[mvnjar](https://www.mvnjar.com/)

xxx/AndroidSDK/tools/`jaxb`

PS:jaxb为新建目录,jar包放在此目录下(放在lib下也可以,配置对就行)

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/GIRLS20191109001236.png)

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/GIRLS20191109001426.png)

Sublime打开Bin下 sdkmanager.bat

第66行 

```
set CLASSPATH=%APP_HOME%\jaxb\activation.jar;%APP_HOME%\jaxb\jaxb-impl.jar;%APP_HOME%\jaxb\jaxb-xjc.jar;%APP_HOME%\jaxb\jaxb-core.jar;%APP_HOME%\jaxb\jaxb-jxc.jar;%APP_HOME%\jaxb\jaxb-api.jar;%APP_HOME%\lib\dvlib-26.0.0-dev.jar;%APP_HOME%\lib\jimfs-1.1.jar;%APP_HOME%\lib\jsr305-1.3.9.jar;%APP_HOME%\lib\repository-26.0.0-dev.jar;%APP_HOME%\lib\j2objc-annotations-1.1.jar;%APP_HOME%\lib\layoutlib-api-26.0.0-dev.jar;%APP_HOME%\lib\gson-2.3.jar;%APP_HOME%\lib\httpcore-4.2.5.jar;%APP_HOME%\lib\commons-logging-1.1.1.jar;%APP_HOME%\lib\commons-compress-1.12.jar;%APP_HOME%\lib\annotations-26.0.0-dev.jar;%APP_HOME%\lib\error_prone_annotations-2.0.18.jar;%APP_HOME%\lib\animal-sniffer-annotations-1.14.jar;%APP_HOME%\lib\httpclient-4.2.6.jar;%APP_HOME%\lib\commons-codec-1.6.jar;%APP_HOME%\lib\common-26.0.0-dev.jar;%APP_HOME%\lib\kxml2-2.3.0.jar;%APP_HOME%\lib\httpmime-4.1.jar;%APP_HOME%\lib\annotations-12.0.jar;%APP_HOME%\lib\sdklib-26.0.0-dev.jar;%APP_HOME%\lib\guava-22.0.jar
```

PS:前6项是追加进去的,如下:

```
%APP_HOME%\jaxb\activation.jar;%APP_HOME%\jaxb\jaxb-impl.jar;%APP_HOME%\jaxb\jaxb-xjc.jar;%APP_HOME%\jaxb\jaxb-core.jar;%APP_HOME%\jaxb\jaxb-jxc.jar;%APP_HOME%\jaxb\jaxb-api.jar;
```

保存OK,继续Bin下执行

```
sdkmanager.bat --update
```

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/GIRLS20191109002643.png)

至此,会出现:

```
 Some Android licenses not accepted.  To resolve this, run: flutter doctor
      --android-licenses
```

根据指示执行:

```
flutter doctor --android-licenses
```

一路y+回车就ok了.

#### 连接Android设备

要准备在Android设备上运行并测试您的Flutter应用，您需要安装Android 4.1（API level 16）或更高版本的Android设备.

1. 在您的设备上启用 **开发人员选项** 和 **USB调试** 。详细说明可在[Android文档](https://developer.android.com/studio/debug/dev-options.html)中找到。
2. 使用USB将手机插入电脑。如果您的设备出现提示，请授权您的计算机访问您的设备。
3. 在终端中，运行 `flutter devices` 命令以验证Flutter识别您连接的Android设备。
4. 运行启动您的应用程序 `flutter run`。

默认情况下，Flutter使用的Android SDK版本是基于你的 `adb` 工具版本。 如果您想让Flutter使用不同版本的Android SDK，则必须将该 `ANDROID_HOME` 环境变量设置为SDK安装目录。

#### 使用Android模拟器

要准备在Android模拟器上运行并测试您的Flutter应用，请按照以下步骤操作：

1. 在您的机器上启用 [VM acceleration](https://developer.android.com/studio/run/emulator-acceleration.html) .

2. 启动 **Android Studio>Tools>Android>AVD Manager** 并选择 **Create Virtual Device**.

3. 选择一个设备并选择 **Next**。

4. 为要模拟的Android版本选择一个或多个系统映像，然后选择 **Next**. 建议使用 *x86* 或 *x86_64* image .

5. 在 Emulated Performance下, 选择 **Hardware - GLES 2.0** 以启用 [硬件加速](https://developer.android.com/studio/run/emulator-acceleration.html).

6. 验证AVD配置是否正确，然后选择 **Finish**。

   有关上述步骤的详细信息，请参阅 [Managing AVDs](https://developer.android.com/studio/run/managing-avds.html).

7. 在 Android Virtual Device Manager中, 点击工具栏的 **Run**。模拟器启动并显示所选操作系统版本或设备的启动画面.

8. 运行 `flutter run` 启动您的设备. 连接的设备名是 `Android SDK built for `,其中 *platform* 是芯片系列, 如 x86.

#### 体验第一个FlutterAPP

创建

一直在creat,发现文件夹已创建了一些文件,就结束了Android Studio进程,重启.直接去文件夹打开项目,然而问题又出现了.

缺少依赖包:

can not get packages from"https://pub.flutter-io.cn/%2xx"

应该是镜像路径问题.复制去看了下:

目的网址应该是https://pub.flutter-io.cn/

后面应该是配置错误.

然后在环境变量中,加入了`/`

```
FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn/
```

```
UB_HOSTED_URL=https://pub.flutter-io.cn/
```

重启OK了.

