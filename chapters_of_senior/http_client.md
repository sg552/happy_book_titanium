# 发送HTTP请求

在Titanium中发送http 请求特别方便。如：

```js
var url = "https://www.tidev.in";

// 定义HTTP请求的回调函数
var xhr = Ti.Network.createHTTPClient({
  onload: function(e) {
    //成功后调用
  },
  onerror: function(e){
    //失败后调用
  }
})

// 注明要使用的HTTP方法和请求的接口地址
xhr.open("GET", url);

// 发送请求
xhr.send();
```

也可以用另一种写法，如下：

```js

var url = "https://www.uubpay.com";

var xhr = Ti.Network.createHTTPClient();

// 成功时调用
xhr.onload = function(e) {
};

// 失败时调用
xhr.error = function(e) { };

// 注明要使用的HTTP方法和请求的接口地址
xhr.open("GET", url);
xhr.send();
```

## 对HTTPClient的封装

通常，我们要对这个函数进行封装。最常见的是，需要对每一个发送出去的请求，都
加上必要的HTTP 参数：

- os_name  客户端的操作系统, ios/android
- os_version 客户端的操作系统版本号,  9.0
- app_version 客户端app的版本号

等等。如下:

```javascript
var append = "osname="+Ti.App.osname+"&osversion="+Ti.App.osversion+"&appversion="+Ti.App.version+"&manufacturer="+Ti.App.manufacturer+"&model="+Ti.App.model+"&memory="+Ti.Platform.availableMemory;
url += url.indexOf("?") > 0 ? "&" + append : "?" + append;
```


## 设置HTTP请求的header

在Titanium中设置header的时候，需要主要的是，用来设置header的setRequestHeader()
必须要在open()方法之后，send()方法之前。

```javascript
var client = Ti.Network.createHTTPClient();
client.open("POST", "http://uubpay.com/files/new");
client.setRequestHeader("Content-type", "text/csv");
client.send();
```

## 上传文件

下面以调用本地相册为例，演示如何上传文件:

```js
var openPhotoGallery = function() {
  Ti.Media.openPhotoGallery({
     success: function(event) {
      //这里面使用了前面提到的发送HTTP请求的方法
      var xhr = Ti.Network.createHTTPClient();
      xhr.onload = function(e) {
        var res = JSON.parse(this.responseText);
        Ti.UI.createAlertDialog({
          title: "Success",
          message: "status code" + this.status
        }).show();
      };

      xhr.open("POST", "http://cms.yuehouse.co/interface/users/change_head_pic");
      xhr.send({
        file: event.media,
        token: "you token here"
      });
    }
  });
};
```

## 下载文件并保存在本地

其实原理很简单，就是远程资源发送一个GET请求

```javascript
var xhr = Ti.Network.HTTPClient();
xhr.onload = function() {

  // 首先要先get到一个handle
  var file = Ti.Filesystem.getFile(Ti.Filesystem.applicationDataDirectory, "myPic.png");

  // 然后将下载下来的图片保存在本地,
  // 注意这里使用的的我们之前提到的responseData,因为是二进制数据
  file.write(this.responseData);
}
// 可以给下载加上一个timeout
xhr.timeout = 10000;
xhr.open("GET", "http://uubpay.com/logo.png");
xhr.send();
```

## 最佳实践

- 务必每次发送请求时，都要在log中有记录。
- 务必留下客户端的信息（操作系统，版本号等）
- 用好callback函数( onload )
- 网络问题引起的错误还是不少的。要写好容错代码，加强健壮性。
- 上传图片时，务必使用progress indicator. 让用户看到进度。
- 建议使用明星框架对HTTPClient的封装。
