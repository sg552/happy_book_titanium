# Capistrano: 自动化部署的利器

## 介绍

<alert>注意： 以下的文档针对的版本是 '2.12.0' </alert>

## 安装方式：

Capistrano 灰常好用。 不过有几个常用的用法还是要留意一下： 参考这个文章：

1. 进入到项目下，

增加下面内容到 `Gemfile` 中：

```ruby
group :development 
  gem 'capistrano', '2.12.0'                                                                                          
  gem 'capistrano-rbenv', '1.0.1'
end
```

2. 安装它

```bash
$ bundle install
```

3.  生成关键性文件：

```bash
$ capify . 
```

会生成两个文件： `Capfile` , `config/deploy.rb`

4. 编辑后者，

5. $ cap deploy:setup 会建立必须的 文件夹

然后 $ cap deploy.

6. 编辑 $ shared/config/database.yml 等其他配置文件。

这里是一个完整的deploy.rb ：

https://github.com/beijing-rubyist/bjrubyist/blob/master/config/deploy.rb

### 使用 命令行 

下面是一个例子， 在命令行中 显示 `User name: ` , 等用户输入完，按回车之后，
把输入的值赋给 `user` 变量。

```ruby
set(:user) { Capistrano::CLI.ui.ask("User name: ") }
```

1. 使用帮助： 
$ cap --help

2. 使用logger，特别是在其他语言调用CAP时，非常有用（例如被fabric 调用）: 

```bash
$ cap setup --logger STDOUT
```

3. 如何使用变量? 

要记得: 使用@. . 例如，我们要设置 "deploy_type" 这个变量： 

```bash
$ cap say_hi --set-before deploy_type=staging
```

然后在 config/deploy.rb 中这样使用：

```ruby
DEFAULT_TYPE = "stable" 

# deploy_type 仅仅在 begin 这个区域中生效, 在rescue, ensure中都不行。 
begin 
  deploy_type 
  puts "deploy_type was set successfully" 
  @deploy_type = deploy_type 
rescue Exception => e 
  puts "deploy_type not set, use default: #{DEFAULT_TYPE}" 
  deploy_type = DEFAULT_TYPE 
  @deploy_type = deploy_type 
end 

task :say_hi do 
  puts "hihihi, var_deploy_type: #{@deploy_type}" 
end
```

输出： 
```bash
deploy_type was set successfully 
============= DEPLOY_PATH: /rails_apps/babble_portal/cutting_edge 
* executing `say_hi' 
hihihi, var_deploy_type: 444
```

最后，使用copy方式：

```
# 脚本中
set :scm, :none
set :repository, "."
set :deploy_via, :copy
```

## capistrano的输出详解
TODO  各种屏幕截图。 建立文件夹， 打包，压缩，上传，解压缩， rake db.. assets等等

## 为什么要用capistrano

流行的工具都是有道理的（ best practices are best in most cases)

1. 版本控制： SVN =>  GIT       ( scm :  from SVN to GIT) 

2. 部署方式： 人肉部署 => Capistrano  

原来项目中用到的是SVN， 就一个分支，也不打TAG。感觉用起来没啥。  ( there's not so much trouble when the project is going under SVN and manual deployment)

现在服务器的配置被运维同学限制了，无法连到SCM 服务器 (同时无法连接到外网，无法连接到很多内部网络，比如LDAP， RADIUS等等）。肿么办????      (but one day, the server was limited its access to the internet, git repo and local LDAP , Radius service... what shall we do? )

如果用SVN的话，就得 用SCP的方式，打包过去，然后修修改改，每次都要人肉来做，还出错。(if using SVN, we have to copy the entire code folder to the target server, easy to make mistake and really painful for me ) 

现在换成了GIT ， 不用capistrano的话，直接在本地把 git-patch 上传过去，然后 git am 就好。(now since we have migrated the SVN to GIT repo, it's very easy to achieve the same goal using 'git-patch' and 'git am' )

用了 capistrano的话，用 deploy_via :scp 的 方式，我每次部署一行命令，自动搞定了。 ( and in capistrano, we just need to use 'deploy_via scp' to do the deployment job ) 

所以，老式的办法，在某些新问题出现的时刻，不是那么得心应手。业界流行的“最佳实践”，在大部分情况下，还是“最佳实践”的。 ^_^    ( the conclusion is:  best practices are always best in most cases. ) 

—— 学习是王道！  ( keep STUDYING everyday! ) 

## capistrano的原理

裸代码:   没有数据库的配置文件,  没有服务器相关的配置文件,  也没有压缩各种css/js , 一般都是从git上直接clone下来的代码. 

### 传统的部署步骤:   

1. ssh 到服务器.  
2. git pull 
3. restart  command ...   


坏处是:  

1. 无法回滚,  
2. 每次都人肉, 特别麻烦. 
(虽然上面3个步骤看似很少, 但是需要一直盯着(比如, ssh 需要10秒, git pull 需要20秒, 
restart 也需要人肉输入, 这些都是时间上的损耗, 而且人肉做重复性的事情, 无趣, 容易出错. )

### 合理的部署是:  

编写好 一个配置文件之后, 运行代码:  `$ cap deploy`  (一个命令) , 之后的所有事情, 
都不用人参与了. 

### 结构: 

1.  有三个角色:       部署人员的机器,           目标服务器,         代码服务器(GIT)

 ( 见譞的本本上的图 ) 

### 每次部署, 都要做的事情: 

1. SSH 到目标服务器
2. 把最新的代码,上传到目标服务器上.  这时候的代码是裸代码( 不能立刻部署, 因为很多配置文件都没有) 

我们不能把配置文件也放到git 里面, 比如: `config/database.yml` , 每个人的数据库的 root , 密码都不一样.  

以及其他的东东(上传文件夹) 

### 原理:  每次部署, 都要用一个文件夹.  (方便回滚) 

回滚的方式有几种: 

1)  code roll back.   (git checkout ...  )    这样不好,很多时候我们无法保证代码是没有被修改的. 被修改之后, checkout .. .会涉及到 代码合并.   这个情况, 在某些 紧急 BUG 出现时, 会特别明显.   
2)  每个release 都用一个文件夹( 里面包含了完整的项目代码, 包括裸代码, 和 各种配置文件) .     比如:  201506,  201505  (时间戳命名)     ,然后, 有一个特殊的 文件夹(softlink, 叫 current )   web服务器 一直使用这个 current 文件夹. (不需要每次都改nginx... thin (rails server) 的配置文件)  , 只需要把 current 这个softlink , 指向不同的 release 文件夹就可以了.  

所以,  capistrano部署下的 文件结构是:

```
/opt/rails_app:  
    current -> /opt/app/happystock_web/releases/20150518030114/ 
    releases/
        20150310010954  
        20150319015536  
        20150518030114
    shared/ 
        assets  
        config  
        files  
        log  
        pids  
        public  
        system
```

( shared 中所保存的内容, 以及部分目录结构, 是由 `config/deploy.rb` 这个配置文件决定的  ) 

3. 准备启动服务器:   
     1. 安装各种新增的rubygem,  

     2.  做必要的数据库迁移.   

     3.  配置各种文件.  

     4.  修改上传文件夹的soft link. 

     5. 其他,每次使用裸代码做部署的时候,都要人肉做的事情.  (修改保存日志的路径,  修改 rails server的配置,  ) 

     6. 编译,压缩 js/ css

4.  重启 服务器.     ( $ nginx -s reload,  $ kill -9 xxx   ,  $ thin start -C config/thin.yml ... )  


## 使用方式

### 第一次运行前的准备工作

1. 自动生成文件夹：

```bash
$ cap deploy:setup  # 建立需要的各种文件夹
```

<alert> 注意： 这里务必记得， 盯紧控制台的输出， 看到它执行完 `mkdir -p ` 之后， 赶紧按
`ctrl + c` 暂停。否则它会默认在远程服务器上安装各种ruby 第三方包，安装各种linux 依赖包。
一不小心就会把服务器环境搞砸了。</alert>

2. 为 `shared` 目录下，增加各种配置文件。 它们只需要被配置一遍

例如： 
```bash
config/thin.yml       # 服务器的配置
config/database.yml   # 数据库的配置
config/log4r.yml      # 日志文件的配置
config/settings.yml   # 系统的配置
```

3. 配置好ruby环境， mysql, thin, nginx 等

```bash
$ bundle exec cap deploy
```

### 以后每次部署， 使用这个就可以

```bash
$ cap deploy     
```

## 无法部署capistrano? Net::SSH::AuthenticationFailed: Authentication failed

对于capistrano 2.12.0, 记得永远显式指定  `net-ssh` 的版本，例如：

```ruby
# Gemfile: 
gem 'net-ssh', '2.7.0'   
```