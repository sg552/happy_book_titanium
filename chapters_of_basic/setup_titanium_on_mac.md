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

## 安装Xcode

Xcode是Mac下的开发工具大杂烩，包括了：

- 可视化开发环境IDE
- iOS 和OS的开发工具
- git等常见的命令行工具
- 常见的第三方工具

我们在Linux下面做开发时，总是需要安装这个lib, 安装那个lib。在Mac下，安装好一个
Xcode就基本万事俱备了。

截止到 2016年2月14日，最新的版本是 2016年2月3日发布的Xcode 7.2.1

打开App store, 注册用户，登陆，然后搜索xcode，下载。

![Xcode下载](/images/basic_setup_download_xcode)

一般来说Xcode需要好几个G，下载的比较久。

安装完Xcode后,我们需要安装Xcode-cli(xcode command),为了在cmd中执行ruby的命令:

```
$ xcode-select --install
```

## 安装 homebrew

跟Linux下的 `apt-get`, `yum` 一样，Mac下也有包管理工具：`homebrew`.

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

我们安装一款下载管理软件："wget"

```
$brew install wget
```

## 安装nvm

具体过程请参考前面的Linux章节.


## 安装appcelerator 和 titanium

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

输入下面命令，可以查看appc的具体说明：
```
$ appc -h
```

有用的，是  login, new, ti, setup 和 info
login: 登陆用户。
new: 新建一个项目
ti:  titanium子命令
setup: 配置环境（包括下载最新ti sdk)
info: 显示当前的配置信息

appc info:

如果没有TI SDK，就安装：

```bash
$ appc info
Appcelerator Command-Line Interface, version 5.1.0
Copyright (c) 2014-2015, Appcelerator, Inc.  All Rights Reserved.

No Mobile SDK found, downloading ...
New version available! 5.1.0.GA

Downloading http://builds.appcelerator.com/mobile-releases/5.1.0/mobilesdk-5.1.0.GA-osx.zip
```

## 安装grunt

```
$ npm install -g grunt-cli
$ npm install -g grunt
```

## 安装coffee

    npm install -g coffee-script


## JDK

安装方式同前面


## VirtualBox

下载地址：

https://www.virtualbox.org/wiki/Downloads

(先注册Genymotion，注册登录后，进入store栏下载)

下载：https://www.genymotion.com/#!/store

教程：https://www.genymotion.com/#!/developers/user-guide

## 单独快速安装某个Titanium SDK

如果你的机器上安装好了：

- appc
- nvm
- node

就希望仅仅安装Titanium的某个版本，那么可以通过下面的方法快速安装。

1. 下载某个Ti SDK文件：http://builds.appcelerator.com
2. 复制并解压缩即可：

```
$ cp <Titanium SDK.zip文件> ~/Library/Application\ Support/Titanium
$ cd ~/Library/Application\ Support/Titanium
$ unzip <Ti SDK.zip文件>
```

就会发现，该SDK.zip文件会释放出两个文件夹：

- mobilesdk
- modules

该方式对Mac 有效。 对于Linux, 需要先定位到Titanium SDK的目录。其他过程一样。
