# Titanium本地存储的几种策略

## 可以使用的文件目录

有四个目录是我们可以使用的：

- Ti.Filesystem.applicationDataDirectory

可写可读，特定于app，完全卸载或者你手动删除之后，文件消失

- Ti.Filesystem.resourecesDirectory

只读，完全卸载或者你手动删除之后，文件消失

- Ti.Filesystem.tempDirectory

可读可写，app完全退出之后，由OS自动将文件内容删除

- Ti.Filesystem.externalStorageDirectory

可读可写，是外部SD或者类似设备的抽象, 在使用之前，可以使用
`Ti.Filesystem.isExternalStorageDirectoryPresent()`(返回值是Boolean类型)
检测设备是否存在。

在移动端的开发中，处理用户登录信息，图片缓存信息，相关本机的信息
都会存在app的手机端。

## Ti.App.Properties

可以把某些信息放到 Ti.App.Properties 文件中。

使用:

tiapp.xml配置，就存在这样的配置:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<ti:app xmlns:ti="http://ti.appcelerator.org">
   <property name="ti.ui.defaultunit" type="string">dp</property>
</ti:app>
```

把值写入文件中：
```js
//利用Ti.App.Properites.setObject将用户的token信息存入本地
Ti.App.Properties.setObject("user_token", 'a1b2c3d4')
```

获取key的值：
```
user_token = Ti.App.Properties.getObject("user_token")
```

## 文件系统访问和存储

Titanium.Filesystem是一个高级文件系统模块，用于访问设备上的文件和目录。

```js
//文件系统的一个目录
var suiteDir = Ti.Filesystem.directoryForSuite('优优宝');
if (!suiteDir) {
 logInApp('目录不存在');
 return;
}
//创建一个空文档: products.txt
var f = Ti.Filesystem.getFile(suiteDir,'products.txt');
//写入内容
f.write('优优宝为大家提供免息贷款!');
```

模拟文件系统存储缓存图片:

```javascript

//在本地的Titanium根目录创建basedir目录,创建一个存储图片的文件
var f = Ti.Filesystem.getFile(
  Ti.Filesystem.applicationDataDirectory, basedir, filename);

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

