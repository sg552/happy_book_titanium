# 命令行基础

Titanium的命令行用起来很简单，

直接输入：

```bash
$ ti
```

会看到命令的提示：

```bash
Usage: titanium <command> [options]

Commands:
   build     builds a project
   clean     removes previous build directories
   config    get and set config options
   create    creates a new project
   help      displays this help screen
   info      display development environment information
   module    displays installed Titanium modules
   plugin    displays installed Titanium CLI plugins
   project   get and set tiapp.xml settings
   sdk       manages installed Titanium SDKs
   setup     sets up the Titanium CLI
```

可以看到它的命令格式，以及每个命令的说明。

如果想看某个命令的具体内容，使用 `$ ti help 某个命令` 的格式，例如：

```bash
$ ti help build
```

## 新建项目

```
$ti create --name=Hi
```


## 运行

这个是最常用的命令了。没有之一。每天就是跟它打交道。
下面的命令是往安卓实体机上打包并运行：

```
$ti build --platform=android --target=device
```

往ios上打包:
```
$ti build --platform=ios --target=device
```
简单吧？

如何往指定设备上安装？例如，我想运行在 iPad 上:

可以使用 `--device-id`参数：

```
$ ti build --platform=ios --device-id

Which simulator do you want to launch your app in?
9.0
   1)  iPad 2          ACD3BE4B-C088-4684-A312-68AAA4DCCDFA
   2)  iPad Retina     DDDB0D41-F801-4B27-8064-D767D6BADFA0
   3)  iPad Air        623BB2FB-546C-48DF-8CD4-FFC20AA7C537
   4)  iPad Air 2      B87C4BA7-8513-4B15-865D-46AABA3E2FF2
   5)  iPhone 4s       D7FD69F1-D91A-440F-A4EC-7CE2DD67FE0C
   6)  iPhone 5        5940887E-75C1-4A60-AE21-97661995EFAF
   7)  iPhone 5s       8EBE7467-58AE-403F-B6C6-117B0EC7CE28
   8)  iPhone 6 Plus   8EDD6548-5BA4-46D8-8A30-5F90EEA83647
   9)  iPhone 6        2649B18C-C1C5-4217-9ADB-49D9398E30DF
  10)  iPhone 6s       B01B4503-F245-4167-9877-20A7BFEFDC95
  11)  iPhone 6s Plus  962AF433-1C00-4918-96C8-3612552FD5A1
```

如果你确定的话，就直接复制你想运行的设备的ID 到命令行中来：

```
$ ti build --platform=ios --device-id=623BB2FB-546C-48DF-8CD4-FFC20AA7C537
```

## 清理

当你发现自己的改动突然不生效了，出现了莫名其妙的错误，那么很可能是过时的文件
导致的。这时候就要做个彻底的清理了。

```
$ ti clean

[DEBUG] No project level plugins to load
[DEBUG] Deleting all platform build directories
[DEBUG] Deleting /workspace/uubpay_mobile/build/android
[DEBUG] Deleting /workspace/uubpay_mobile/build/build_android.log
[DEBUG] Deleting /workspace/uubpay_mobile/build/build_iphone.log
[DEBUG] Deleting /workspace/uubpay_mobile/build/iphone
[INFO]  Project cleaned successfully in 421ms
```

可以看到，这个命令把 build 目录下的所有内容都删掉了。

那么下一次build的时候，编译的时间就会特别漫长。

## 检查环境

```
$ti setup
Enter ctrl-c at any time to quit.

──────────────────────┤ Main Menu ├───────────────────────

   1)  quick    Quick Setup
   2)  check    Check Environment
   3)  user     User Information
   4)  app      New App Defaults
   5)  network  Network Settings
   6)  cli      Titanium CLI Settings
   7)  sdk      Titanium SDK Settings
   8)  ios      iOS Settings
   9)  android  Android Settings
  10)  exit     Exit
Where do you want to go?
```

可以看到，出现了10个选项。 从名字上看都很清晰了。可以根据你的需要来做各种设置。
在首次开发时特别重要。

例如，我想查看android的环境是否配置好了，就可以在这个界面下，进入到 `9) android`

```
──────────────────┤ Check Environment ├───────────────────

Node.js
  ✓  node               installed (v0.10.37)
  ✓  npm                installed (v1.4.28)

Titanium CLI
  ★  cli                new version v5.0.6 available (currently v5.0.5)

Titanium CLI Dependencies
  ✓  async              up-to-date (v1.4.2)
  ✓  colors             up-to-date (v1.1.2)
  ...其他内容省略

Titanium SDK
  ✓  latest sdk         installed (v4.0.0.GA)
  ✓  selected sdk       up-to-date (v4.0.0.GA)

Mac OS X Environment
  ✓  CLI Tools          installed

iOS Environment
  ✓  Xcode              installed (7.0)
  ✓  iOS SDK            installed (9.0)
  ✓  WWDR cert          installed
  !  developer cert     not found
  !  distribution cert  not found
  !  dev provisioning   not found
  !  dist provisioning  not found

Android Environment
  ✓  sdk                installed (/workspace/coding_tools/android-sdk-macosx)
  !  tools              untested version 24.4.1; may or may not work
  ✓  platform tools     installed (v23.1)
  ✓  build tools        installed (v23.0.2)
  ✓  adb                installed /workspace/...
  ... 其他内容省略


Java Development Kit
  ✓  jdk                installed (v1.7.0)
  ✓  java               installed /Library/...
  ✓  javac              installed /Library/...
  ✓  keytool            installed /Library/...
  ✓  jarsigner          installed /Library/...

Intel® Hardware Accelerated Execution Manager (HAXM)
  ✓  compatible
  !  installed          not found; install HAXM to use Android x86 emulator

Network
  ✓  online
  -  no proxy server configured
  ✓  Network connection test
  ✓  Java-based connection test

Directory Permissions
  ✓  home directory
  ✓  titanium config directory
  ✓  titanium sdk install directory
  ✓  temp directory
```

各种配置，一应俱全。

## 鸡肋的 appc

在titanium 5.0 或以后，它的子命令的一部分并入了`appc` 命令中。比如登陆。

```
$ appc login
```

具体的appc 命令如下：

```bash
$ appc
  Usage: appc cmd [options]


  Commands:

    access <get|set> [options]           get or set access in platform
    config <get|set|list> [key] [value]  get, set, and list configuration settings
    generate [options]                   create a component
    install [options]                    install a component
    login [options]                      login to platform
    logout [options]                     logout of platform
    new [options]                        create a new project
    owner <add|list|rm> <user>           add, list, and remove owners for a component
    org <add|list|rm> <org>              add, list, and remove orgs for a component
    platform [options]                   runs a appcelerator platform API
    publish [options]                    publish a project or component
    run <app|server> [options]           run a project
    search [options]                     search for components
    setup [options]                      setup your environment
    switch <org> [options]               switch logged in org
    ti [cmd] [options]                   execute titanium commands
    unpublish [options]                  unpublish a project or component
    user <add|list|rm> <user>            add, list, and remove users for a component
    whoami                               get the current platform user
    info                                 Display development environment information
    help [cmd]                           display help for [cmd]
```

虽然让之前的ti命令更加专注于 移动开发，但是appc 这个命令却包罗万象，跟远程服务
有密切的联系。比如，用户必须登陆才能使用，用户做的很多事情都需要跟美国服务器
打交道。 所以， `appc` 这个命令 除了用来登陆, 其他的我们都用不上。
