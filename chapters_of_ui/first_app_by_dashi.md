ti -h 可以看到所有的ti 命令

ti 是 titanium 的缩写。  也是命令行中的主要命令（跟rails 一样）
ti 也是 appcelerator公司的主要产品。

到了titanium SDK 5.0的阶段时， appcelerator 公司就把ti命令，变成了appc 命令。（
回头大家再看一下）。 ti命令应该还能用。

$ ti setup

就可以检查你的机器是否准备好了环境。

```bash

──────────────────┤ Check Environment ├───────────────────

Node.js
  ✓  node               installed (v0.10.37)
  ✓  npm                installed (v1.4.28)

Titanium CLI
  ★  cli                new version v5.0.5 available (currently v5.0.4)

Titanium CLI Dependencies
  ✓  async              up-to-date (v1.4.2)
  ✓  colors             up-to-date (v1.1.2)
  ✓  fields             up-to-date (v0.1.24)
  ✓  humanize           up-to-date (v0.0.9)
  ✓  longjohn           up-to-date (v0.2.9)
  ✓  moment             up-to-date (v2.10.6)
  ✓  node-appc          up-to-date (v0.2.31)
  ✓  request            up-to-date (v2.62.0)
  ✓  semver             up-to-date (v5.0.3)
  ✓  sprintf            up-to-date (v0.1.5)
  ✓  temp               up-to-date (v0.8.3)
  ✓  winston            up-to-date (v1.0.2)
  ✓  wrench             up-to-date (v1.5.8)

Titanium SDK
  ✓  latest sdk         installed (v4.0.0.GA)
  ✓  selected sdk       up-to-date (v4.0.0.GA)

Mac OS X Environment
  ✓  CLI Tools          installed

iOS Environment
  ✓  Xcode              installed (6.2)
  ✓  iOS SDK            installed (8.2)
  ✓  WWDR cert          installed
  !  developer cert     not found
  !  distribution cert  not found
  !  dev provisioning   not found
  !  dist provisioning  not found

Android Environment
  ✓  sdk                installed (/Users/zmcNotafraid/workspace/android-sdk-macosx)
  ✓  tools              installed (v24.1.2)
  ✓  platform tools     installed (v22)
  ✓  build tools        installed (v22.0.1)
  ✓  adb                installed /Users/zmcNotafraid/workspace/android-sdk-macosx/platform-tools/adb
  ✓  android            installed /Users/zmcNotafraid/workspace/android-sdk-macosx/tools/android
  ✓  emulator           installed /Users/zmcNotafraid/workspace/android-sdk-macosx/tools/emulator
  ✓  mksdcard           installed /Users/zmcNotafraid/workspace/android-sdk-macosx/tools/mksdcard
  ✓  zipalign           installed /Users/zmcNotafraid/workspace/android-sdk-macosx/build-tools/22.0.1/zipalign
  ✓  aapt               installed /Users/zmcNotafraid/workspace/android-sdk-macosx/build-tools/22.0.1/aapt
  ✓  aidl               installed /Users/zmcNotafraid/workspace/android-sdk-macosx/build-tools/22.0.1/aidl
  ✓  targets            installed (10 found)
  !  avds               no avds found
  !  ndk                Android NDK not found

Java Development Kit
  ✓  jdk                installed (v1.7.0)
  ✓  java               installed /Library/Java/JavaVirtualMachines/jdk1.7.0_79.jdk/Contents/Home/bin/java
  ✓  javac              installed /Library/Java/JavaVirtualMachines/jdk1.7.0_79.jdk/Contents/Home/bin/javac
  ✓  keytool            installed /Library/Java/JavaVirtualMachines/jdk1.7.0_79.jdk/Contents/Home/bin/keytool
  ✓  jarsigner          installed /Library/Java/JavaVirtualMachines/jdk1.7.0_79.jdk/Contents/Home/bin/jarsigner

Intel® Hardware Accelerated Execution Manager (HAXM)
  ✓  compatible
  !  installed          not found; install HAXM to use Android x86 emulator

Network
  ✓  online
  -  no proxy server configured
  ✕  https://www.appcelerator.com (HTTP status: 404) is unreachable
  ✕  https://www.google.com (HTTP status: 404) is unreachable
  ✓  Java-based connection test

Directory Permissions
  ✓  home directory
  ✓  titanium config directory
  ✓  titanium sdk install directory
  ✓  workspace directory
  ✓  temp directory
```

所以，这个机器，是不能打包和发布ios应用的。所以我们暂时用android平台来开发。


$ ti create test_ti_app

```bash
Titanium Command-Line Interface, CLI version 5.0.4, Titanium SDK version 5.0.0.GA
Copyright (c) 2012-2015, Appcelerator, Inc.  All Rights Reserved.

Please report bugs to http://jira.appcelerator.org/

What type of project would you like to create?
 1)  Titanium App
 2)  Titanium Module
 3)  Apple Watch™ App
Select a type by number or name [app]:

```

1. 是app.  2. 是module (用来作为app的一部分，职责是调用原生java/oc 代码) .3 apple watch

```bash
Target platform (all|android|mobileweb|iphone|ipad|windows) [all]:

Project name: test_app

App ID: com.uubpay

Your company/personal URL: uubpay.com

Directory to place project [/Users/zmcNotafraid/workspace]:
```

于是开始建立代码。

```bash

$ cd ti_app
$ find .

>find .
.
./DefaultIcon.png
./LICENSE
./README
./Resources
./Resources/android
./Resources/android/appicon.png
./Resources/android/default.png
./Resources/android/images
./Resources/android/images/res-long-land-hdpi
./Resources/android/images/res-long-land-hdpi/default.png
./Resources/android/images/res-long-land-ldpi
./Resources/android/images/res-long-land-ldpi/default.png
./Resources/android/images/res-long-port-hdpi
./Resources/android/images/res-long-port-hdpi/default.png
./Resources/android/images/res-long-port-ldpi
./Resources/android/images/res-long-port-ldpi/default.png
./Resources/android/images/res-notlong-land-hdpi
./Resources/android/images/res-notlong-land-hdpi/default.png
./Resources/android/images/res-notlong-land-ldpi
./Resources/android/images/res-notlong-land-ldpi/default.png
./Resources/android/images/res-notlong-land-mdpi
./Resources/android/images/res-notlong-land-mdpi/default.png
./Resources/android/images/res-notlong-port-hdpi
./Resources/android/images/res-notlong-port-hdpi/default.png
./Resources/android/images/res-notlong-port-ldpi
./Resources/android/images/res-notlong-port-ldpi/default.png
./Resources/android/images/res-notlong-port-mdpi
./Resources/android/images/res-notlong-port-mdpi/default.png
./Resources/app.js
./Resources/iphone
./Resources/iphone/Default-568h@2x.png
./Resources/iphone/Default-667h@2x.png
./Resources/iphone/Default-Landscape-736h@3x.png
./Resources/iphone/Default-Landscape.png
./Resources/iphone/Default-Landscape@2x.png
./Resources/iphone/Default-Portrait-736h@3x.png
./Resources/iphone/Default-Portrait.png
./Resources/iphone/Default-Portrait@2x.png
./Resources/iphone/Default.png
./Resources/iphone/Default@2x.png
./Resources/KS_nav_ui.png
./Resources/KS_nav_views.png
./tiapp.xml

```

过滤一下，之后可以看到：

```
find .
.
./DefaultIcon.png
./LICENSE
./README
./Resources
./Resources/android
./Resources/android/appicon.png
./Resources/android/default.png
./Resources/android/images
./Resources/android/images/res-notlong-port-mdpi/default.png
./Resources/app.js
./Resources/iphone
./Resources/iphone/Default@2x.png
./Resources/KS_nav_ui.png
./Resources/KS_nav_views.png
./tiapp.xml
```

关键的文件是：

- tiapp.xml : 整个app的配置文件
- Resources/app.js : 就是app源代码。所有的代码都可以写到里面。


```bash
$ ti build

Titanium Command-Line Interface, CLI version 5.0.4, Titanium SDK version 5.0.0.GA
Copyright (c) 2012-2015, Appcelerator, Inc.  All Rights Reserved.

Please report bugs to http://jira.appcelerator.org/

Target platform to build for:
 1)  android
 2)  ios
 3)  mobileweb
 4)  windows
Enter # or platform name: 1

Mon Oct 26 2015 11:20:42 GMT+0800 (CST)

Operating System
  Name                        = Mac OS X
  Version                     = 10.10.5
  Architecture                = 64bit
  # CPUs                      = 4
  Memory                      = 8589934592

Node.js
  Node.js Version             = 0.10.37
  npm Version                 = 1.4.28

Titanium CLI
  CLI Version                 = 5.0.4

Titanium SDK
  SDK Version                 = 5.0.0.GA
  SDK Path                    = /Users/zmcNotafraid/Library/Application Support/Titanium/mobilesdk/osx/5.0.0.GA
  Target Platform             = android

....
```

于是 Genymotion自动启动。等一下，就跑起来了。


## titanium中的UI基础。

最上级的东东，应该是： window, ?? 大概有4种。

启动流程已经讲了。

# appc 与 ti命令的关系

在titanium 3.x和以前， 命令行只有一个命令： ti
在titanium 4.0 以后， 由于appcelerator的关系，他们把ti的一部分命令 提取出来，
外加一些新命令，放到了 appc 命令中。
例如：

原来：  $ ti build/new
现在：  $ appc ti build/new

# 需要到appc后台注册个你的应用

如果发现这个消息：
```
[ERROR] Application not registered.
```
就需要你到后台，把这个app注册了。

第一次进入后台，发现你是没有告诉appcelerator公司，你新建了任何的app。

```(图片）
You don't have any apps yet!

Don't worry, it's easy to get started creating apps using the Platform. It should take you only a few minutes to create an app. Once you do, your dashboard will have data here. You can see a demo of the dashboard below.
```

# app开发与 web开发的主要区别

参考；http://siwei.me/blog/posts/web-mobile-web-mobile-development-core

我们现在的优势： （只有明星我们知道）

(初期可以不考虑这条）1. 把代码放在远程服务器上。 这样，就做到了不需要每次都发布app。 修改bug，直接在服务器端修改。

2. 改动瞬间生效。（ 有两个页面。一个页面是第二个页面的入口, （在1#页面点击按钮，进入到2#页面））
我们每次修改2#页面后，退回到1#页面，再点击按钮，2#页面的改动马上就可以看到了！）

3. 不需要做机型适配。 ( 小手机上看起来什么样，大手机就什么样。 16:9 的什么样。
16：10的也按照原比例进行拉伸，所以，看起来是差不多的）

4. 不需要做跨平台的适配（有个前提，大家在使用UI组件的时候，最好使用通用的组件。
）

可以节省我们大量的时间。 让我们的开发变得快乐。

实际的情况：

一天，最多改20次（实际上一天改一个UI 页面就差不多了） 甚至，改一个BUTTON的样式，都
特别痛苦。 黄敏的生产率很高。 但是，他当时调一个页面，需要3天。

开发门槛很高，需要大家具备的能力有：

1. 熟悉所有的UI组件
2. 知道 app 的内在架构（就是通过 event来驱动的，手点点点。。才能看到各种页面）
3. 知道 如何调用 native的功能。 照相，调用相册，发push 等等。(module)
4. 知道如何调试。 它的调试信息，不如rails可读性那么强。所以大家要具备经验。
5. 每个人都要知道如何编译，打包啊。做到，每天下班前，都要给产品经理一个最新的版本。
6. 使用到了很多js的功能（requirejs -- 拆分的, underscore, coffeescript ... )
