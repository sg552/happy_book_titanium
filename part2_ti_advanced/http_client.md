Hello, HTTPClient!

Titanium实现了五个HTTP的方法，分别是GET, POST, PUT, DELETE, PATCH

常用的就两个GET和POST。

成功发送一个http请求总共分三步:
- create an HTTP client
- open an HTTP connection
- send an HTTP request

处理response的方式也有三种：
- this.responseText, 把response当做纯文本(raw text)，最常用的是用来接收JSON字符串
- this.responseXML, 把response当做xml对象处理
- this.responseData, 把response当做Blob(Binary Large Object),二进制大对象

### 下面演示如何在手机端发送一个HTTP请求：

```javascript
var url = "https://www.baidu.com";

// 定义HTTP请求的回调函数
var xhr = Ti.Network.createHTTPClient({
  onload: function(e) {
// 这里是一个回调函数，当请求成功是调用
  onerror: function(e){
// 这里是一个回调函数， 当请求失败是调用
  }
 }
})

// 注明要使用的HTTP方法和请求的接口地址
xhr.open("GET", url);
// 发送请求
xhr.send();
```

### 我们项目中还普遍存在另一种写法，如下：
```javascript

var url = "https://www.baidu.com";

var xhr = Ti.Network.createHTTPClient();
xhr.onload = function(e) {
// 这里是一个回调函数，当请求成功是调用
  };

  xhr.error = function(e) {
// 这里是一个回调函数， 当请求失败是调用
}
// 注明要使用的HTTP方法和请求的接口地址
xhr.open("GET", url);
xhr.send();
```

### 有的时候，设置HTTP请求的的header是非常必要的。

在Titanium中设置header的时候，需要主要的是，用来设置header的setRequestHeader()必须要要在open()方法之后，send()方法之前。

```javascript
var client = Ti.Network.createHTTPClient();
client.open("POST", "http://yourservr.com/files/new");
client.setRequestHeader("Content-type", "text/csv");
client.send();
```

### 使用HTTP Client上传(upload)文件
下面以调用本地相册为例，演示如何上传文件。
```javascript
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

### 下载文件并保存在本地
下面以下载图片来演示，在Titanium中如何通过HTTP请求来下载文件

其实原理很简单，就是向你的资源发送一个GET请求
```javascript
var xhr = Ti.Network.HTTPClient();
xhr.onload = function() {
// 首先要先get到一个handle
var file = Ti.Filesystem.getFile(Ti.Filesystem.applicationDataDirectory, "myPic.png");
// 然后将下载下来的图片保存在本地, 注意这里使用的的我们之前提到的responseData,因为是二进制数据
file.write(this.responseData);
}
// 可以给下载加上一个timeout
xhr.timeout = 10000;
xhr.open("GET", "http://myserver.com/path/to/your/resources");
xhr.send();
```

### 可以使用的文件目录
提到将文件保存到本地，就不得不提一下，对于一部手机的OS，都有哪些目录是我们开发者可以使用的。

在Titanium中，主要由四个目录是我们可以使用的：
- Ti.Filesystem.applicationDataDirectory: 可写可读，特定于app，完全卸载或者你手动删除之后，文件消失
- Ti.Filesystem.resourecesDirectory: 只读，完全卸载或者你手动删除之后，文件消失
- Ti.Filesystem.tempDirectory, 可读可写，app完全退出之后，由OS自动将文件内容删除
- Ti.Filesystem.externalStorageDirectory: 可读可写，是外部SD或者类似设备的抽象, 在使用之前，可以使用Ti.Filesystem.isExternalStorageDirectoryPresent()(返回值是Boolean类型)检测设备是否存在

TODO:结合做的项目的实际代码进行说明。
