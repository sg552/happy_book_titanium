# Hello world 跑起来

我们可以使用 `appc create` 来创建一个app. 但是更多时候我们用ti 这个命令。

ti 是 titanium 的缩写。  也是命令行中的主要命令（跟rails 一样）

到了titanium SDK 5.0的阶段时， appcelerator 公司就把ti命令中的用户相关部分（
login, logout等）抽离出来，变成了appc 命令。

ti命令变的更加纯粹，只用于开发。

可以直接用

```bash
$ ti create ...
```
也可以写成

```
$ appc ti create ...
```

我们一般都用前者。 因为脱离了appc，用起来更顺手。

## 检查环境

```
$ ti setup
```

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
  ...

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
  ...
  !  avds               no avds found
  !  ndk                Android NDK not found

Java Development Kit
  ✓  jdk                installed (v1.7.0)
  ✓  java               installed /Library/Java/JavaVirtualMachines/jdk1.7.0_79.jdk/Contents/Home/bin/java

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
  ...
```

所以，这个机器，是不能打包和发布ios应用的。所以我们暂时用android平台来开发。

## 创建App

```bash
$ ti create test_ti_app

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

App ID: com.test
Your company/personal URL: test.com
Directory to place project [.]:
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

下面我们试着运行这个“裸”项目：

```bash
$ ti build
```

下面是控制台的输出：
```
Titanium Command-Line Interface, CLI version 5.0.4, Titanium SDK version 5.0.0.GA
Copyright (c) 2012-2015, Appcelerator, Inc.  All Rights Reserved.

Target platform to build for:
 1)  android
 2)  ios
 3)  mobileweb
 4)  windows
Enter # or platform name: 1

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

![hello](/images/basic_tutorial_hello.png)

## titanium中的UI基础。

启动流程已经讲了。

