# Titanium本地存储的几种策略

##本地存储的意义:在移动端的开发中，处理用户登录信息，图片缓存信息，相关本机的信息
  在实际app开发中，都会存在app的手机端，那么本地存储显得相关重要。

###1.轻量级持久性与属性

    TODO

###2.SQLite数据库的存储

  ```javascript

    var db = Ti.Database.open('weatherDB'); //创建一个叫做weatherDB的数据库


    var db = Ti.Database.open('TiBountyHunter');
    db.execute('CREATE TABLE IF NOT EXISTS fugitives(id INTEGER PRIMARY KEY, name TEXT, captured INTEGER, url TEXT, capturedLat REAL, capturedLong REAL);');
    db.close(); //db.execute() 操作会执行相应的sql语句

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

    TODO
