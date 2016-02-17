# 搭建Titanium开发环境

最合适的环境是Mac, 因为它同时支持两个平台。

次之的是Linux, 可以开发Android应用。

Windows 还是放弃吧.

主要步骤分成：

- 安装JDK
- 安装NVM和Node
- 安装VirtualBox 和Genymotion
- 安装Appcelerator和Titanium命令行, Alloy
- 安装grunt, grunt-watch, coffeescript
- (仅iOS)安装Xcode 和 Xcode 命令行
- (仅iOS)安装homebrew
- (仅android)安装Android SDK
- (仅android)安装Ant

# 在Mac下安装Titanium

需要安装两种环境

- Android 开发环境
- iOS 开发环境

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

![Xcode下载](/images/basic_setup_download_xcode.png)

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

## 安装NVM 和Node

node 必须安装 v0.10.37

可以使用NVM(Node Version Manager)来安装。

### 下载NVM

```bash
git clone https://github.com/creationix/nvm.git ~/.nvm && cd ~/.nvm && git checkout `git describe --abbrev=0 --tags`
```

### 启动时加载：

把下面这行代码放到： `~/.bashrc` 或 `~/.bash_profile`,  `~/.zshrc` 中。

```bash
source ~/.nvm/nvm.sh
```

### 运行NVM
```
$ nvm
```
后，能看到
```
Node Version Manager

Note: <version> refers to any version-like string nvm understands.
.....
```
说明安装成功了。

注意： 不能使用 `$ which nvm` 来验证安装是否成功。因为即使成功了也不会有
`$ which nvm` 返回结果。

### 使用nvm

- 列出所有可以安装的版本：

```bash
$ nvm list-remote
```

- 列出本地安装好了的版本：

```bash
$ nvm list
```

- 安装 0.10.37 版本

```bash
$ nvm install v0.10.37
```

- 使用：

```bash
# 把这句命令放到 ~/.bashrc 中。
$ nvm alias default 0.10.37
```


## 安装appcelerator 和 titanium

你必须在appcelerator上注册：

1. http://www.appcelerator.com/

在 "start free with email" 中，输入你的邮箱即可：

![注册](/images/basic_setup_register_input_email.png)

我们就会看到页面有了反馈：

![要求查看邮箱](/images/basic_setup_check_email.png)

邮件内容如下：

![邮件内容](/images/basic_setup_register_info_from_email.png)

点击其中的链接，进入到完善账户信息页面：

![完善账户信息](/images/basic_setup_appc_account.png)

我们就进入到了平台：https://platform.appcelerator.com/

先安装 appcelerator, 这个命令用于登陆等用户操作：

```bash
$ sudo npm install appcelerator -g
```

配置 appc
```bash
$ appc setup

Finding latest version ...5.1.0 ✓
Validating security checksum ✓
Installing ... ✓
Compiling platform native modules ...
└ ws/utf-8-validate ...  ✓
└ chokidar/fsevents ...  ✓
└ chokidar/fsevents ...  ✓
...
```

过程中会要求你输入appcelerator的账号和密码：
输入完后，还要求你输入一个authorize code. 这个时候必须要检查下邮箱。
```bash
Appcelerator Login required to continue ...

? Appcelerator ID: shensiwei@sina.com
? Password: ******
```

上面的登陆步骤也可以使用 `appc login` 这个命令单独做：
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
- login: 登陆用户。
- new: 新建一个项目
- ti:  titanium子命令
- setup: 配置环境（包括下载最新ti sdk)
- info: 显示当前的配置信息

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

再安装titanium sdk，这是我们日常开发的核心：
```bash
$ appc ti sdk install 5.2.0.GA
```

## 安装grunt

```bash
$ npm install -g grunt-cli
$ npm install -g grunt
```

## 安装coffee

```bash
$ npm install -g coffee-script
```

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

# 在Linux上搭建Titanium开发环境

## 安装JDK

- JDK 只能安装Oracle的，不是Oracle的不行。(Open JDK肯定不行)
- JDK 只能安装1.7， 其他的都不行.

请自行google搜索:  'oracle jdk 1.7', 最新版本就是。

http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html 不好找链接的朋友,请看:

```bash
$ wget TODO
```

把JDK解压到： /workspace/jdk1.7.0_67之后:

只要设置好下面三个变量就可以了。（具体的值需要自行修改）

```bash
export JAVA_HOME="/workspace/jdk1.7.0_67"
export CLASSPATH="$JAVA_HOME/lib:."
export PATH="$PATH:$JAVA_HOME/bin"
```

$ vim ~/.bashrc, 把下面的变量都加进去：

```bash
( 如果是从0 开始配置环境的话，ADT_PATH 先不要设置，因为这个时候还没下载好。  )
JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64/
ANT_HOME=/sg552/workspace/ant-1.9.4
PATH=$PATH:$JAVA_HOME/bin:$ANT_HOME/bin:
```

```bash
$ source ~/.bashrc
$ java -version
```
能看到下面这些信息，就说明JDK已经安装好了。
```bash
 java version "1.7.0_79"
 Java(TM) SE Runtime Environment (build 1.7.0_79-b15)
 Java HotSpot(TM) 64-Bit Server VM (build 24.79-b02, mixed mode)
```

## 安装 Android SDK, NDK.

必须在安装好JDK之后安装。

```bash
$ 下载并安装JDK
$ install android sdk
$ wget http://mirrors.hust.edu.cn/apache/ant/binaries/apache-ant-1.9.4-bin.zip ,
$ unzip <apache.zip>
```

解压缩android SDK，设置ADT:

```
ADT_PATH=/sg552/adt-bundle-linux-x86-20130522/
ANDROID_HOME=$ADT_PATH/sdk
PATH=$PATH:$ANDROID_HOME/platform-tools
PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/build-tools:$ANDROID_HOME/platform-tools

```

开始配置Android:
```
$ android (该命令来自于：$ANDROID_HOME/tools/android)
```
记得先配置好代理先。 （见  ssl-edge的用法）

![设置Android SDK 代理](/images/basic_setup_android_gui_proxy.jpg)

基本上， tools 全选，

android 4.4 以上的全选。

![选择SDK 版本号](/images/basic_setup_android_sdk_gui.jpg)

extras 全选

![选择好extra](/images/basic_setup_android_extras.jpg)

然后就是漫长的下载等待了。

下载好了之后，需要安装其他的。

### android sdk文件依赖缺失

项目npm install之后，开始运行项目时出现的错误；貌似可能和android sdk
安装的时候有关系，因为出现了某个library依赖文件的错误，
可能需要更新或者是系统缺少了这个依赖文件．

```
[ERROR] Failed to package application:

 /home/lglove/android-sdk-linux/build-tools/22.0.1/aapt: error while loading shared libraries: libstdc++.so: cannot open shared object file: No such file or directory
```

```
$ sudo apt-get install lib32stdc++6 lib32z1 lib32z1-dev
$ sudo apt-get install libstdc++6:i386
```


## 安装 Titanium Command Line

命令行是所有操作的基础. 很多错误无法通过GUI页面显示出来, 而command line
就能让我们很方便的debug .

eclipse 虽好，但是我只喜欢 命令行。 因为IDE 把太多的debug细节都隐藏了。与其让eclipse输出debug信息，不如直接让我自己动手。

refer to:  http://docs.appcelerator.com/titanium/3.0/#!/guide/Setting_up_the_Titanium_CLI-section-37520113_SettinguptheTitaniumCLI-InstalltheCLI

### 安装 node module: titanium

titanium 是个 node package:

```bash
$ npm install -g titanium
```

再安装titanium SDK:

```bash
$ titanium sdk install
```

配置titanium SDK

```bash
$ titanium setup

# 然后会跳出很多配置项供你选择.

──────────────────────┤ Main Menu ├───────────────────────

   1)  quick    Quick Setup
   2)  check    Check Environment
   3)  user     User Information
   4)  app      New App Defaults
   5)  network  Network Settings
   6)  cli      Titanium CLI Settings
   7)  sdk      Titanium SDK Settings
   8)  android  Android Settings
   9)  exit     Exit
Where do you want to go?
```

最重要的是 第二个项目, check, 它会很详细的告诉你哪些东西安装好了,哪些木有.

我们输入'k', 进入到 "check"步骤:

```bash
──────────────────┤ Check Environment ├───────────────────

Node.js
  ★  node               new version v0.10.33 available! (currently v0.10.32)
  ★  npm                new version v2.1.9 available! (currently v1.4.28)

Titanium CLI
  ★  cli                new version v3.4.1 available (currently v3.4.0)

Titanium CLI Dependencies
  ✓  async              up-to-date (v0.2.10)
  ✓  colors             up-to-date (v0.6.2)
  ✓  fields             up-to-date (v0.1.17)
  ✓  humanize           up-to-date (v0.0.9)
  ...

Titanium SDK
  ★  latest sdk         new version v3.4.1.GA available! (currently v3.4.0.GA)
  ✓  selected sdk       up-to-date (v3.4.0.GA)

Android Environment
  ✓  sdk                installed (/workspace/android-sdk-linux)
  ✓  tools              installed (v23.0.2)
  ...

Java Development Kit
  ✓  jdk                installed (v1.7.0)
  ...
```


最后,测试:

```bash
$ titanium create --name MyFirstProject
$ cd <MyFirstProject>
$ titanium build
```

## 安装 NDK

Android NDK 用来编译Titaium native module.

refer to:  https://developer.android.com/tools/sdk/ndk/index.html

```bash
$ wget http://dl.google.com/android/ndk/android-ndk-r10d-linux-x86_64.bin
$ chmod a+ <ndk_file>
```

就会自动解压缩。

```bash
$ ./<ndk_file>
```

然后安装gperf：

```bash
$ sudo apt-get install gperf
```

然后设置 PATH

```bash
ANDROID_NDK="/workspace/coding_tools/android-ndk-r10d"
PATH=$PATH:$ANDROID_NDK
```

最后，输入命令，如果可以得到结果就算成功:

```bash
$ ndk-build
Android NDK: Could not find application project directory !
Android NDK: Please define the NDK_PROJECT_PATH variable to point to it.
/workspace/coding_tools/android-ndk-r10d/build/core/build-local.mk:148: *** Android NDK: Aborting    .  Stop.
```

设置好 titanium 中的ndk:

```
$ ti setup
(下面的步骤略)
```

## 安装Alloy

```bash
$ npm install -g alloy
```

## 安装 grunt:

refer to:  http://gruntjs.com/getting-started

自动化永远是我们程序员所追求的方式.

对于c 有 make ,对于 ruby 有 rake, 对于 java 有ant, maven, ivry,
对于js 则是 grunt.

Rails 或者 Titanium 自带的一些命令虽然好用, (` $ alloy compile`,
`$ ti build/clean`) 但是粒度略小. 比如我要用jade 编写xml, 用coffee编写js ,
就需要在 运行 `$ alloy compile` 之前先运行 一个 脚本:

```bash
# file name:  compile_my_coffee_to_js:
#compile coffee
cd app/controllers/
coffee -bc *.coffee
cd ../../

cd app/controllers/home/
cat home_market.coffee home_master.coffee home_me.coffee home_competition.coffee home_community.coffee home_version.coffee home_frame.coffee | coffee -bc --stdio  > ../home.js
cd ../../../
```

其实每次运行这个脚本就很烦. 而且可读性差. 而且跟grunt语言相比有很大的缺点(
最突出的就是不如grunt专业和全面), 将来维护的话必然是个大坑. (
想起之前有运维同学专门手写了个 shell 部署脚本的程序, 花了好几天时间,
结果写出来的东西跟capistrano 相差甚远, 不但可读性差(shell v.s. ruby)
而且无法回滚.

所以 , 有好轮子就要用. 对自身也是个提高.

再之, 考虑到 grunt 本身就是个国宝级项目 (github 9133 个关注), 我们是务必要用的.

安装:

```bash
$ npm install -g grunt grunt-cli

$ which grunt
/Users/sg552/.nvm/v0.10.37/bin/grunt
```


## 安装 genymotion:

http://siwei.me/blog/posts/genymotion-mobile-app-using-genymotion

注意事项：

- 使用Genymotion时， 务必要先在GUI中登录，否则会出现adb 使用不了 设备的情况
- 使用 adb 之前，务必要安装 i386的组件（对于ubuntu13+) ，否则会出现 adb 程序运行不了的情况（ 类似32位程序无法在64位机器上运行）
- 安装 genymotion 需要的各种patch , see: http://forum.xda-developers.com/showthread.php?t=2528952

