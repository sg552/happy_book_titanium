# 对数据库的操作

手机上的数据库都是SQLite。它没有太强大的功能和性能，但是足以满足我们对数据
的查询了。

下面是基本操作

```js
// 打开或创建数据库: uubpay
var db = Ti.Database.open('uubpay');

// 新建一个table
db.execute('CREATE TABLE IF NOT EXISTS fugitives(id INTEGER PRIMARY KEY, name TEXT, captured INTEGER, url TEXT, capturedLat REAL, capturedLong REAL);');

// 关闭数据库
db.close();

// 安装数据库（或者新建数据库文件）
var db = Ti.Database.install('/mydata/weatherDB', 'weatherDB');

// insert 语句
db.execute('INSERT INTO city (name,continent,temp_f,temp_c,condition_id) VALUES (?,?,?,?,?)', importName, importContinent, importTempF, importTempC, dbConditionId);//插入相关数据

// 查询数据
var cityWeatherRS = db.execute('SELECT id,name,continent FROM city');

while (cityWeatherRS.isValidRow())
{
  var cityId = cityWeatherRS.fieldByName('id');
  var cityName = cityWeatherRS.fieldByName('name');
  var cityContinent = cityWeatherRS.fieldByName('continent');
  Ti.API.info(cityId + ' ' + cityName + ' ' + cityContinent);
  // 使用 .next() 方法来把记录指针指向下一条
  cityWeatherRS.next();
}

// 关闭数据库连接
cityWeatherRS.close();
```
