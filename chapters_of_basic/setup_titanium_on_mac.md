# 在Mac下安装Titanium

需要安装两种环境

- Android 开发环境
- iOS 开发环境

## 安装  titanium sdk, android sdk的快速方法

## Titanium SDK

$ cp 5.1.1.GA 到： /Users/你的用户名/Library/Application Support/Titanium
$ 进入到该目录，运行unzip. 就会把两个关键性的目录：modules, mobilesdk 中的内容
复制过去了。（需要覆盖的时候，就果断全部覆盖)

Titanium SDK 的版本自从2014年下半年开始就迭代的非常快。我们务必跟上步伐。

## Android SDK

cp android-23 到： $ANDROID_HOME/platforms 目录下

1.看看你的mac是否自带Xcode，如果没有则需要去App Store下载

  PS：由于Apple的最新升级，现在在AppStore下载的最新的Xcode7.0已经不在支持Titanium5.0.0.GA以下的SDK版本了；所以，如果你要使用最新的Xcode，那么必须的使用Titanium-sdk >= 5.0.0.GA的SDK，否则就下载7.0以下的Xcode；下载地址为Apple开发者官方网址，所以你需要注册Apple Developer账号。网址（注册登录后下载）：https://developer.apple.com/downloads/

  如果选择在网页中搜索下载，那么需要对自己的mac进行第三方软件允许安装权限设置：

```
System Preferences -> General -> Allow apps downloaded from -> (选中)Anywhere
```

  安装完Xcode后,我们需要安装Xcode-cli(xcode command),为了在cmd中执行ruby的命令:

```
xcode-select --install
```

2.安装完Xcode后,我们需要安装一个软件下载管理工具homebrew;
以后如果要安装其他软件包直接使用[brew install 插件名]命令来执行就行

```
  ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

  安装完毕后,我们需要安装一个wget插件,使用http请求获取某个软件包的安装源(即识别url请求)

```
  brew install wget
```

3.安装nvm[node version manage](需要通过nvm来安装node，指定我们需要的node
版本安装，更方便有效；nvm会自带安装npm[node pakage manage])

具体过程请参考前面的Linux章节.

4.安装完nvm，我们开始安装titanium

  如果你已经下载sdk包,那么只要将你所下载的sdk包放到以下指定的文件路径里就可以了(
  因为我们通过:titanium sdk config [任意sdk的路径:path]命令来指定sdk的路径失效了):

  ```
  cd /Users/hufeipeng/Library/Application Support/Titanium
  mkdir mobilesdk
  cd mobilesdk
  mkdir osx
  ```

  然后将你所下载的sdk包cp这个路径里就行了:
  ```
  /Users/hufeipeng/Library/Application Support/Titanium/mobilesdk/osx/3.5.1.GA
  ```

  或者通过命令行安装: (参考：https://web.appcelerator.com/product/cli）

  - 安装appcelerator

  ```
  sudo npm install appcelerator -g
  appc setup
  ```

  - 安装titanium sdk

  ```
  $ titanium sdk install 3.5.1.GA(如果需要较新的sdk,可以换成4.1.0.GA)
  ```

  - 配置 appc
  ```
  $ appc setup
  Finding latest version ...5.1.0 ✓
  Validating security checksum ✓
  Installing ... ✓
  Compiling platform native modules ...
  └ extract-opts/typechecker ... ✓
  └ bunyan/dtrace-provider ...  ✓
  └ extract-opts/typechecker ...  ✓
  └ socket.io-client/ws ...  ✓
  └ appc-ldapjs/dtrace-provider ...  ✓
  └ bunyan/dtrace-provider ...  ✓
  └ appc-ldapjs/dtrace-provider ...  ✓
  └ ws/bufferutil ...  ✓
  └ ws/utf-8-validate ...  ✓
  └ chokidar/fsevents ...  ✓
  └ chokidar/fsevents ...  ✓

  Appcelerator Login required to continue ...

  ? Appcelerator ID: shensiwei@sina.com
  ? Password: ******
  ```

期间会问你要用户名和密码。
输入完后，还要求你输入一个authorize code. 这个时候必须要检查下邮箱。

```
$ appc login
Appcelerator Command-Line Interface, version 5.1.0
Copyright (c) 2014-2015, Appcelerator, Inc.  All Rights Reserved.

Appcelerator Login required to continue ...

? Appcelerator ID: shensiwei@sina.com
? Password: ******

? Please enter the authorization code you received via your email at shensiwei@sina.com: 9907
sina.com: 9907
This computer is now authorized: Mac OSX Serial Number: C02Q4FH5FVH3
You can deauthorize this computer by logging out with appc logout
sina.com: 9
Generating Developer Certificate and Private/Public Keys...
shensiwei@sina.com logged into organization shensiwei@sina.com [100020049]
```

appc -h :
```
$ appc -h
Appcelerator Command-Line Interface, version 5.1.0
Copyright (c) 2014-2015, Appcelerator, Inc.  All Rights Reserved.


  Usage: appc cmd [options]


  Commands:

    access <get|set> [options]           get or set access in platform
    config <get|set|list> [key] [value]  get, set, and list configuration settings
    generate [options]                   create a component
    help [cmd]                           display help for [cmd]
    info                                 Display development environment information
    install [options]                    install a component
    login [options]                      login to platform
    logout [options]                     logout of platform
    new [options]                        create a new project
    org <add|list|rm> <org>              add, list, and remove orgs for a component
    owner <add|list|rm> <user>           add, list, and remove owners for a component
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
```
有用的，是  login, new, ti, setup 和 info
login: 登陆用户。
new: 新建一个项目
ti:  titanium子命令
setup: 配置环境（包括下载最新ti sdk)
info: 显示当前的配置信息

appc info:
如果没有TI SDK，就安装：
```
$ appc info
Appcelerator Command-Line Interface, version 5.1.0
Copyright (c) 2014-2015, Appcelerator, Inc.  All Rights Reserved.

No Mobile SDK found, downloading ...
New version available! 5.1.0.GA

Downloading http://builds.appcelerator.com/mobile-releases/5.1.0/mobilesdk-5.1.0.GA-osx.zip

```

    npm install -g grunt-cli
    npm install -g grunt

  ③安装coffee
    npm install -g coffee-script

11.JDK/JRE

11.JDK: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

   JRE: https://www.java.com/en/download/mac_download.jsp

12.android sdk文件依赖缺失

   项目npm install之后，开始运行项目时出现的错误；貌似可能和android sdk安装的时候有关系，因为出现了某个library依赖文件的错误，可能需要更新或者是系统缺少了这个依赖文件．


   [ERROR] Failed to package application:

   [ERROR]
 /home/lglove/android-sdk-linux/build-tools/22.0.1/aapt: error while loading shared libraries: libstdc++.so: cannot open shared object file: No such file or directory

   sudo apt-get install lib32stdc++6 lib32z1 lib32z1-dev
   sudo apt-get install libstdc++6:i386


13.virtualBox下载：
   https://www.virtualbox.org/wiki/Downloads

   (先注册Genymotion，注册登录后，进入store栏下载)

   下载：https://www.genymotion.com/#!/store

   教程：https://www.genymotion.com/#!/developers/user-guide
