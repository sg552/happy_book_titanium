# 搭建Titanium开发环境

windows的朋友，放弃吧！　下面的安装仅限　linux , mac.

TODO 增加titanium 版本

## 安装 jdk: (必须是oracle 1.7) : http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html 不好找链接的朋友,请看:

```bash
$ wget http://download.oracle.com/otn-pub/java/jdk/7u75-b13/jdk-7u75-linux-x64.tar.gz
```

## 安装nvm / nodejs

node的安装不难，官方给的是直接下载安装包。

对于一些比较特殊的情况（比如说centos的某些server版本），需要编译源代码，兼容性才好。

但是有些情况需要特定的node版本，比如 stss.  必须 v0.10.37才能装的好。 而 titanium似乎也对node 版本有要求。

node 官方的最新版本是 0.12.2

所以， 需要一个多版本的node管理工具就特别重要。

NVM 就是我们的选择。 （跟当初的RVM  , rbenv 一样）

### 下载NVM

```bash
git clone https://github.com/creationix/nvm.git ~/.nvm && cd ~/.nvm && git checkout `git describe --abbrev=0 --tags`
```

### 启动时加载：

```bash
# 把下面这行代码放到： ~/.bashrc  ~/.bash_profile ~/.zshrc 中。
source ~/.nvm/nvm.sh
```

### 运行：
`$ nvm`

注意： 不能使用 `$ which nvm` 来验证安装是否成功。因为即使成功了也不会 有 `$ which nvm` 返回结果。

### 使用

1.列出所有可以安装的版本：

```bash
$ nvm list-remote
```

2.列出本地安装好了的版本：

```bash
$ nvm list
```

3.安装：

```bash
$ nvm install v0.10.37
```

4.使用：

```bash
# 把这句命令放到 ~/.bashrc 中。
$ nvm alias default 0.10.32
```

官方的例子：

```
  nvm install v0.10.32                  Install a specific version number
  nvm use 0.10                          Use the latest available 0.10.x release
  nvm run 0.10.32 app.js                Run app.js using node v0.10.32
  nvm exec 0.10.32 node app.js          Run `node app.js` with the PATH pointing to node v0.10.32
  nvm alias default 0.10.32             Set default node version on a shell
```

### 删除

直接手动删掉：~/.nvm,  ~/.npm ~/.bower 即可。

再安装nodejs (nodejs 0.10.37， 在 必须是这个版本，否则会出现 stss （npm 插件） 不能正常工作, 安装完之后，npm就自动装好了））

## 安装android SDK, NDK. 参考： http://siwei.me/blog/posts/0-android-titanium

> 注意： 第一步一定要有个代理。

然后记得 只能安装 `oracle JDK 1.7`.  1.8 的不行（虽然TI的官方说行）。
不是ORACLE的也不行（比如open jdk)

```bash
$ install oracle JDK 1.7
$ install android sdk
$ wget http://mirrors.hust.edu.cn/apache/ant/binaries/apache-ant-1.9.4-bin.zip ,
$ unzip <apache.zip>
```

安装JDK 非常简单， 只要设置好下面三个变量就可以了。 （具体的值需要自行修改）

```bash
 export JAVA_HOME="/workspace/jdk1.7.0_67"
 export CLASSPATH="$JAVA_HOME/lib:."
 export PATH="$PATH:$JAVA_HOME/bin"
```

$ vim ~/.bashrc, 把下面的变量都加进去：

```bash
( 如果是从0 开始配置环境的话，ADT_PATH 先不要设置，因为这个时候还没下载好。  )
ADT_PATH=/sg552/adt-bundle-linux-x86-20130522/
JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64/
ANT_HOME=/sg552/workspace/ant-1.9.4
ANDROID_HOME=$ADT_PATH/sdk
PATH=$PATH:$ANDROID_HOME/platform-tools
PATH=$PATH:$JAVA_HOME/bin:$ANT_HOME/bin:$ANDROID_HOME/tools:$ANDROID_HOME/build-tools:$ANDROID_HOME/platform-tools
PATH=$PATH:$ANDROID_HOME/build-tools/android-4.2.2/
```

```bash
   $ source ~/.bashrc
   $ java -version  ( 就可以看到输出一堆信息）
   $ android  （ 就可以看到打开一个android配置窗口）
```

记得先配置好代理先。 （见  ssl-edge的用法）

（如果你已经从其他同学那里copy 到了需要的android sdk, 那么可以跳过这一步）

![Set Android Sdk Manager Proxy](http://siwei.me/system/images/W1siZiIsIjIwMTUvMDMvMjIvMDBfMDBfMzdfODE3X3NldF9hbmRyb2lkX3Nka19tYW5hZ2VyX3Byb3h5LnBuZyJdXQ/set%20android%20sdk%20manager%20proxy.png)

基本上， tools 全选，

android 4.3 以上的全选。

![Screenshot From 2015 03 22 07:59:02](http://siwei.me/system/images/W1siZiIsIjIwMTUvMDMvMjIvMDBfMDFfMDVfMzU3X1NjcmVlbnNob3RfZnJvbV8yMDE1XzAzXzIyXzA3XzU5XzAyLnBuZyJdXQ/Screenshot%20from%202015-03-22%2007%3A59%3A02.png)

extras 全选

![Screenshot From 2015 03 22 07:59:09](http://siwei.me/system/images/W1siZiIsIjIwMTUvMDMvMjIvMDBfMDFfMDVfNTMzX1NjcmVlbnNob3RfZnJvbV8yMDE1XzAzXzIyXzA3XzU5XzA5LnBuZyJdXQ/Screenshot%20from%202015-03-22%2007%3A59%3A09.png)

然后就是漫长的下载等待了。

下载好了之后， 需要安装其他的。

$ nodejs:    下载源代码， 编译。 不要直接用编译好的。 有时候会出现莫名其妙的错误 https://nodejs.org/download/

```bash
$ wget  http://nodejs.org/dist/v0.10.36/node-v0.10.36-linux-x64.tar.gz
（最好用 0.10.32 左右   因为 0.12 太新了，安装不上 npm）
$ tar zxvf ...
$ ./configure && make && make install ...
```

## 安装 titanium command line:

命令行是所有操作的基础. 很多 错误无法通过GUI页面显示出来, 而command line 就能很方便的debug .

eclipse 虽好，但是我只喜欢 命令行。 因为IDE 把太多的debug细节都隐藏了。与其让eclipse输出debug信息，不如直接让我自己动手。

refer to:  http://docs.appcelerator.com/titanium/3.0/#!/guide/Setting_up_the_Titanium_CLI-section-37520113_SettinguptheTitaniumCLI-InstalltheCLI

1.安装 node module: titanium

```bash
$ npm install -g titanium
```

2.在命令行登陆titanium:

```bash
$ titanium login (记得先注册)

sg552@siwei-linux-notebook:/workspace$ titanium login
Titanium Command-Line Interface, CLI version 3.4.0, Titanium SDK version 3.4.0.GA
Copyright (c) 2012-2014, Appcelerator, Inc.  All Rights Reserved.

Please report bugs to http://jira.appcelerator.org/

Username: shensiwei@sina.com
Password: ******
Logged in successfully
```

3.安装titanium SDK

```bash
$ titanium sdk install
```

4.配置titanium SDK

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
  ✓  jade               up-to-date (v0.35.0)
  ✓  longjohn           up-to-date (v0.2.4)
  ✓  moment             up-to-date (v2.4.0)
  ✓  node-appc          up-to-date (v0.2.14)
  ✓  optimist           up-to-date (v0.6.1)
  ✓  request            up-to-date (v2.27.0)
  ✓  semver             up-to-date (v2.2.1)
  ✓  sprintf            up-to-date (v0.1.4)
  ✓  temp               up-to-date (v0.6.0)
  ✓  winston            up-to-date (v0.6.2)
  ✓  wrench             up-to-date (v1.5.8)

Titanium SDK
  ★  latest sdk         new version v3.4.1.GA available! (currently v3.4.0.GA)
  ✓  selected sdk       up-to-date (v3.4.0.GA)

Android Environment
  ✓  sdk                installed (/workspace/android-sdk-linux)
  ✓  tools              installed (v23.0.2)
  ✓  platform tools     installed (v20)
  ✓  build tools        installed (v20)
  ✓  adb                installed /workspace/android-sdk-linux/platform-tools/adb
  ✓  android            installed /workspace/android-sdk-linux/tools/android
  ✓  emulator           installed /workspace/android-sdk-linux/tools/emulator
  ✓  mksdcard           installed /workspace/android-sdk-linux/tools/mksdcard
  ✓  zipalign           installed /workspace/android-sdk-linux/build-tools/20.0.0/zipalign
  ✓  aapt               installed /workspace/android-sdk-linux/build-tools/20.0.0/aapt
  ✓  aidl               installed /workspace/android-sdk-linux/build-tools/20.0.0/aidl
  ✓  targets            installed (3 found)
  ✓  avds               installed (1 found)
  !  ndk                Android NDK not found

Java Development Kit
  ✓  jdk                installed (v1.7.0)
  ✓  java               installed /workspace/coding_tools/jdk1.7.0_67/bin/java
  ✓  javac              installed /workspace/coding_tools/jdk1.7.0_67/bin/javac
  ✓  keytool            installed /workspace/coding_tools/jdk1.7.0_67/bin/keytool
  ✓  jarsigner          installed /workspace/coding_tools/jdk1.7.0_67/bin/jarsigner

Intel® Hardware Accelerated Execution Manager (HAXM)
  ✓  compatible
  !  installed          not found; install HAXM to use Android x86 emulator

Network
  ✓  online
  ✓  proxy server enabled
  ✓  http request test
  ✓  https request test

Directory Permissions
  ✓  home directory
  ✓  titanium config directory
  ✓  titanium sdk install directory
  ✓  temp directory
```


最后,测试:

```bash
$ titanium create --name MyFirstProject
$ cd <MyFirstProject>
$ titanium build
```

## 安装 NDK

refer to:  https://developer.android.com/tools/sdk/ndk/index.html

```bash
$ wget http://dl.google.com/android/ndk/android-ndk-r10d-linux-x86_64.bin
$ chmod a+ <ndk_file>
```

就会自动解压缩。

```bash
$ ./<ndk_file>
```

然后安装这个东东：

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

对于c 有 make ,对于 ruby 有 rake, 对于 java 有ant, maven, ivry, 对于js 则是 grunt.

Rails 或者 Titanium 自带的一些命令虽然好用, (` $ alloy compile`,  `$ ti build/clean`) 但是粒度略小. 比如我要用jade 编写xml, 用coffee编写js , 就需要在 运行 `$ alloy compile` 之前先运行 一个 脚本:

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

其实每次运行这个脚本就很烦. 而且可读性差. 而且跟grunt语言相比有很大的缺点( 最突出的就是不如grunt专业和全面), 将来维护的话必然是个大坑. ( 想起之前有运维同学专门手写了个 shell 部署脚本的程序, 花了好几天时间,结果写出来的东西 跟capistrano 相差甚远, 不但可读性差(shell v.s. ruby, 呵呵) 而且无法回滚.

所以 , 有好轮子就要用. 对自身也是个提高.

再之, 考虑到 grunt 本身就是个国宝级项目 (github 9133 个关注), 我们是务必要用的.

安装:

```bash
$ npm install -g grunt grunt-cli
```

运行:

需要本地目录有 `Gruntfile` ( 跟Makefile, Rakefile 极度类似) , `package.json` (跟 Gemfile 极度类似)

Gruntfile.(js|cofee):  定义了要运行的各种方法 . 下面是个例子:

```javascript
module.exports = function(grunt) {

  // Project configuration.
  grunt.initConfig({
    pkg: grunt.file.readJSON('package.json'),
    uglify: {
      options: {
        banner: '/*! <%= pkg.name %> <%= grunt.template.today("yyyy-mm-dd") %> */\n'
      },
      build: {
        src: 'src/<%= pkg.name %>.js',
        dest: 'build/<%= pkg.name %>.min.js'
      }
    }
  });

  // Load the plugin that provides the "uglify" task.
  grunt.loadNpmTasks('grunt-contrib-uglify');

  // Default task(s).
  grunt.registerTask('default', ['uglify']);

};
```

package.json: 跟Gemfile一样, 定义了各种依赖包. 通过 $ grunt-init 或者 $npm init  来生成.下面是个例子:

```json
{
  "name": "my-project-name",
  "version": "0.1.0",
  "devDependencies": {
    "grunt": "~0.4.5",
    "grunt-contrib-jshint": "~0.10.0",
    "grunt-contrib-nodeunit": "~0.4.1",
    "grunt-contrib-uglify": "~0.5.0"
  }
}
```

在 Gruntfile 中,可以使用 <% %> 来引用配置文件的各种信息:

```javascript
grunt.initConfig({
  pkg: grunt.file.readJSON('package.json'),
  uglify: {
    options: {
      banner: '/*! <%= pkg.name %> <%= grunt.template.today("yyyy-mm-dd") %> */\n'
    },
    build: {
      src: 'src/<%= pkg.name %>.js',
      dest: 'build/<%= pkg.name %>.min.js'
    }
  }
});
```

加载任务( load task) :

```javascript
grunt.loadNpmTasks('grunt-contrib-uglify');
加载自定义任务，　并且默认运行：

  // 默认提供了　plugin:
  grunt.registerTask('default', ['uglify']);

  // 如果没有提供plugin的话，就直接　写出来：
  // A very basic default task.
  grunt.registerTask('default', 'Log some stuff.', function() {
    grunt.log.write('Logging some stuff...').ok();
  });
```

## 安装 genymotion:

http://siwei.me/blog/posts/genymotion-mobile-app-using-genymotion


注意事项：

- 使用Genymotion时， 务必要先在GUI中登录，否则会出现adb 使用不了 设备的情况
- 使用 adb 之前，务必要安装 i386的组件（对于ubuntu13+) ，否则会出现 adb 程序运行不了的情况（ 类似32位程序无法在64位机器上运行）
- 安装 genymotion 需要的各种patch , see: http://forum.xda-developers.com/showthread.php?t=2528952


## 安装 android sdk:

$ wget https://dl.google.com/android/android-sdk


## 对于mac, 按照上面的步骤配置完后，还要配置（ 申请账号，下载证书等等） mac开发对应的东东：

http://siwei.me/blog/categories/–5?utf8=%E2%9C%93&title=%E5%8F%91%E5%B8%83%E5%BA%94%E7%94%A8&commit=%E6%90%9C%E7%B4%A2

## 安装之后,使用 $ti setup , 即可知道自己差哪儿缺哪儿了.


