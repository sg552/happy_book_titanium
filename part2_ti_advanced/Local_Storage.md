# Titanium本地存储的几种策略

##本地存储的意义:在移动端的开发中，处理用户登录信息，图片缓存信息，相关本机的信息
  在实际app开发中，都会存在app的手机端，那么本地存储显得相关重要。

###1.轻量级持久性与属性
   ####Ti.App.Properties简介与使用
  简介:Titanium应用程序属性模块用于存储应用程序的相关数据，这些数据在持续超过应用程序会话和设备电源周期的属性/值对中。

  使用(使用Ti.App.Properties模拟用户登录信息存储本地的实战技巧):

  ```javascript
   1.tiapp.xml配置
   <?xml version="1.0" encoding="UTF-8"?>
   <ti:app xmlns:ti="http://ti.appcelerator.org">
       <property name="ti.ui.defaultunit" type="string">dp</property>
   </ti:app>

    2.我们在Titanium中定义了一个用来处理用户登录请求的方法sing_in_process

       function sing_in_process(){
          remote_data = JSON.parse(this.responseText) //解析获取远程的json数据
          user_token = remote_data.result.token       //获取用户token信息
          user_id = remote_data.result.id             //获取用户的id信息
          user_name = remote_data.result.user_name    //获取用户的用户名
          user_phone = remote_data.result.user_phone  //获取用户的手机号码
          Ti.App.Properties.setObject("user_token", user_token) //利用Ti.App.Properites.setObject将用户的token信息存入本地
          Ti.App.Properties.setObject("id", user_id)
          Ti.App.Properties.setObject("user_name",user_name)
          Ti.App.Properties.setObject("user_phone",user_phone)
       }

    3.读取本地用户的信息判断用户是否有登录的权限

        user_phone = Ti.App.Properties.getObject("user_phone")
        if user_phone
           console.info "你可以sign_out哦"
        else
           $.sign_out.setVisible(false)
           console.info "赶紧去注册吧，注册了才能sign out哦"

    4.总结:
        以上三步模拟了Titanium中使用Ti.App.Properties 实现本地信息存储的过程。第二步中发送http请求步骤省略，仅仅是从处理
        请求的结果进行了代码分析，如果对Titanium发送HTTP请求有什么疑问，可以看相关的HTTP请求章节。

  ```

###2.SQLite数据库的存储

  ```javascript

    var db = Ti.Database.open('weatherDB'); //创建一个叫做weatherDB的数据库


    var db = Ti.Database.open('TiBountyHunter'); //创建数据库

    db.execute('CREATE TABLE IF NOT EXISTS fugitives(id INTEGER PRIMARY KEY, name TEXT, captured INTEGER, url TEXT, capturedLat REAL, capturedLong REAL);');

    db.close();  //db.execute() 操作会执行相应的sql语句

    var db = Ti.Database.install('/mydata/weatherDB', 'weatherDB'); //安装数据库

    db.execute('INSERT INTO city (name,continent,temp_f,temp_c,condition_id) VALUES (?,?,?,?,?)', importName, importContinent, importTempF, importTempC, dbConditionId);//插入相关数据

    var cityWeatherRS = db.execute('SELECT id,name,continent FROM city');

    //检索数据
    while (cityWeatherRS.isValidRow())
    {
      var cityId = cityWeatherRS.fieldByName('id');
      var cityName = cityWeatherRS.fieldByName('name');
      var cityContinent = cityWeatherRS.fieldByName('continent');
      Ti.API.info(cityId + ' ' + cityName + ' ' + cityContinent);
      cityWeatherRS.next();
    }
    cityWeatherRS.close();


  ```

###3.文件系统访问和存储

   Titanium.Filesystem是一个高级文件系统模块，用于访问设备上的文件和目录。

   官方案例:

  ```javascript
   var suiteDir = Ti.Filesystem.directoryForSuite('group.appc.Sharing'); //文件系统的一个目录
   if (!suiteDir) {
     logInApp('Suite Directory not found, check Entitlements.');
     return;
   }
   var f = Ti.Filesystem.getFile(suiteDir,'emptyfile.txt'); //创建一个suiteDir的目录，和一个emptyfile.txt文档
   f.write('The file is no longer empty!'); //写入文档的语句

  ```
   实战演示(模拟文件系统存储缓存图片):

  ```javascript

   //在本地的Titanium根目录创建basedir目录,创建一个存储图片的文件
   var f = Ti.Filesystem.getFile(Ti.Filesystem.applicationDataDirectory, basedir, filename);
   //获取远程的图片信息同时写入文件系统
   var req = Ti.Network.createHTTPClient();
   req.open('GET', url);
   req.onload = function() {
     if (req.status == 200) {
       f.write(req.responseData);
     }
   }
  req.send();
  ```




