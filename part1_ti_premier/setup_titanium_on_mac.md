PS：安装Chrome浏览器，并配置翻墙，这是首先要做的。

下载ssledge插件（王涛提供的脚本插件）：http://pan.baidu.com/s/1bn5CrBx

下载完成后，打开Chrome，点击Chrome最右侧的菜单栏，选择moretools中的extensions，将下载的脚本插件拖入到里面就行了。



1.看看你的mac是否自带Xcode，如果没有则需要去App Store下载



  PS：由于Apple的最新升级，现在在AppStore下载的最新的Xcode7.0已经不在支持Titanium5.0.0.GA以下的SDK版本了；所以，如果你要使用最新的Xcode，那么必须的使用Titanium-sdk >= 5.0.0.GA的SDK，否则就下载7.0以下的Xcode；下载地址为Apple开发者官方网址，所以你需要注册Apple Developer账号。网址（注册登录后下载）：https://developer.apple.com/downloads/



  如果选择在网页中搜索下载，那么需要对自己的mac进行第三方软件允许安装权限设置：


  System Preferences -> General -> Allow apps downloaded from -> (选中)Anywhere



  安装完Xcode后,我们需要安装Xcode-cli(xcode command),为了在cmd中执行ruby的命令:



    xcode-select --install



2.安装完Xcode后,我们需要安装一个软件下载管理工具homebrew;以后如果要安装其他软件包直接使用[brew install 插件名]命令来执行就行



    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"



  安装完毕后,我们需要安装一个wget插件,使用http请求获取某个软件包的安装源(即识别url请求)



    brew install wget

3.配置vim



    下载：http://siwei.me/system/resources/W1siZiIsIjIwMTQvMTAvMjEvMDlfNTdfMDdfODA3X2RvdF92aW1fZm9sZGVyLnppcCJdXQ/dot_vim_folder.zip


    解压到自己的根目录下：unzip /Users/hufeipeng/Downloads/dot_vim_folder.zip



    下载.vimrc：wget http://siwei.me/system/resources/BAhbBlsHOgZmSSIjMjAxNC8wMS8xOS8wNV81MV8zOF82NjVfLnZpbXJjBjoGRVQ/.vimrc



4.安装完Xcode后，我们接下来要为mac配置zshell(oh-my-zsh，其他的还有.bashrc/.bash_profile等等，这里建议使用zshell)



  oh-my-zsh:


  git clone https://github.com/robbyrussell/oh-my-zsh.git



  下载完毕后，做一些修改：



    ①设置oh-my-zsh为安全的隐藏文件


      mv oh-my-zsh .oh-my-zsh


   ②将zshell配置的“相对路径” 改为“绝对路径”，并增加输出符号“>”效果


     cd .oh-my-zsh

            vi themes/robbyrussell.zsh-theme



     修改第二行：


       原配置  PROMPT='${ret_status}%{$fg_bold[green]%}%p %{%fg[cyan]%}%c %{%fg.........} .... %%{$reset_color%}'

       修改后  PROMPT='${ret_status}%{$fg_bold[green]%}%p %{%fg[cyan]%}%d %{%fg.........} .... %%{$reset_color%}>'



   ③将模板zshrc.zsh-template文件copy成本地的.zshrc配置文件


     cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc


     chsh -s /bin/zsh



5.安装完oh-my-zsh后，我们解下来要安装nvm[node version manage](需要通过nvm来安装node，指定我们需要的node版本安装，更方便有效；nvm会自带安装npm[node pakage manage])


  参考大师的blog，按照步骤来，不会有太大的问题:


  地址：siwei.me/blog/posts/nvm-node



6.安装完nvm，我们开始安装titanium



  如果你已经下载sdk包,那么只要将你所下载的sdk包放到以下指定的文件路径里就可以了(因为我们通过:titanium sdk config [任意sdk的路径:path]命令来指定sdk的路径失效了):


    cd /Users/hufeipeng/Library/Application Support/Titanium


    mkdir mobilesdk


    cd mobilesdk


    mkdir osx



    然后将你所下载的sdk包cp这个路径里就行了:
 /Users/hufeipeng/Library/Application Support/Titanium/mobilesdk/osx/3.5.1.GA



    或者通过命令行安装:



      ①安装titanium

        npm install -g titanium


     ②安装titanium sdk


       titanium sdk install 3.5.1.GA(如果需要较新的sdk,可以换成4.1.0.GA)



7.gem配置



  gem install bundler



  碰到问题:(看样子好像是"SSL"代理而导致"资源包"下载卡住引起的,因此我们要换个下载源)


  Unable to download data from https://rubygems.org/ -Error::ECONNRESET: Connection reset by peer - SSL_connect(https://rubygems.org/quick/Marshal.4.8/bundler-1.10.6.gemspec.rz)



  解决办法:


    参考:(很有用,可以把其他的问题都看看)
        www.iyunv.com/thread-97282-1-1.html



        gem source -r https://rubygems.org/


        gem source -a https://ruby.taobao.org/


        gem install bundler --no-doc



8.gem安装rails



  gem install rails --version=4.1.6



9.安装titanium相关的工具



  ①tishadow



    npm install -g tishadow



    有一个隐藏问题:


      Unable to write config file /Users/hufeipeng/.titanium/config.json


      Please ensure the Titanium CLI has access to modify this file



  ②grunt(现在我们的项目中,一般都有package.json这个文件,里面列出了项目运行需要安装的插件工具[一般指定了具体的版本];项目clone到本地后,进到根目录运行npm install命令就可以了)



    npm install -g grunt-cli


    npm install -g grunt



  ③安装coffee



    npm install -g coffee-script



  ③安装stss



    npm install -g stss



    注意:



      -g参数是global全局引用的意思,就是说以后所有的项目都可以引用全局配置好的这个插件(有些项目可能需要特别的版本,所有才有了package.json这个文件)



    如果安装完上述插件,运行ti build可能会报alloy:command not found这个错误,那么执行一下这个命令(该问题本来不应该出现的,还没找到根本原因):



    npm install -g alloy



10.安装mysql



   (如果需要自己个性化设置安装自己的mysql,可以google[mac install mysql server]找教程,过程很详细)



  在mysql的官网中下载mysql安装包:



     http://dev.mysql.com/downloads/file.php?id=458460



   安装完mysql,建议安装mysql work bench,即mysql可视化工作台插件,这个可以在官网里下载:


          http://dev.mysql.com/downloads/file.php?id=457796



   注意:



     安装完mysql后,需要在.zsh中配置mysql的一些句柄命令(王涛支持)



     配置完成后,运行某个后台项目,执行db:create命令时可能会报一个mysql的错误,问题好像出现在了mysql library文件依赖的配置上,原因目前还不是很清楚:



       problem---->



         rake aborted!

         LoadError: dlopen(/Library/Ruby/Gems/2.0.0/gems/mysql2-0.3.18/lib/mysql2/mysql2.bundle, 9): Library not loaded: libmysqlclient.18.dylib


       answer---->



         cd /usr/local


         export DYLD_LIBRARY_PATH=/usr/local/mysql-5.1.67-osx10.6-x86_64/lib:$DYLD_LIBRARY_PATH

11.JDK/JRE



11.JDK: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

   JRE: https://www.java.com/en/download/mac_download.jsp



12.android sdk文件依赖缺失



   项目npm install之后，开始运行项目时出现的错误；貌似可能和android sdk安装的时候有关系，因为出现了某个library依赖文件的错误，可能需要更新或者是系统缺少了这个依赖文件．



   problem---->


   [ERROR] Failed to package application:

   [ERROR]
 /home/lglove/android-sdk-linux/build-tools/22.0.1/aapt: error while loading shared libraries: libstdc++.so: cannot open shared object file: No such file or directory



   answer---->


   sudo apt-get install lib32stdc++6 lib32z1 lib32z1-dev

   sudo apt-get install libstdc++6:i386

13.VirtualBox/Genymotion



13.virtualBox下载：
   https://www.virtualbox.org/wiki/Downloads



   (先注册Genymotion，注册登录后，进入store栏下载)


   下载：https://www.genymotion.com/#!/store


   教程：https://www.genymotion.com/#!/developers/user-guide
