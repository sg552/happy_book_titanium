#HTTPClient

##简介
Titanium实现了五个HTTP的方法，分别是GET, POST, PUT, DELETE, PATCH。常用的就两个GET和POST。

成功发送一个http请求总共分三步:

- create an HTTP client
- open an HTTP connection
- send an HTTP request

处理response的方式也有三种：

- this.responseText, 把response当做纯文本(raw text)，最常用的是用来接收JSON字符串
- this.responseXML, 把response当做xml对象处理
- this.responseData, 把response当做Blob(Binary Large Object),二进制大对象

##实例

下面是在手机端发送一个HTTP请求的具体实现代码：

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

也可以用另一种写法，如下：

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
##httpClient的封装

参数说明:

- url: 需要请求的参数
- load_callback: 响应成功的回调函数
- error_callback: 响应失败的回调函数
- method: 请求方式GET,POST等等
- args: http请求的参数,GET请求不需要参数

```javascript
function http_call(url, load_callback, error_callback, method, args){
	var xhr = Ti.Network.createHTTPClient();
	xhr.timeout = Ti.App.timeout;
	xhr.onerror = function() {
		if (error_callback)
			error_callback(this);
		else
			show_timeout_dlg(xhr, url);
	};
	xhr.onload = function() {
		if (load_callback)
			load_callback(this);
	};

	if (url.indexOf(Ti.App.helloworld) == 0){
		var append = "osname="+Ti.App.osname+"&osversion="+Ti.App.osversion+"&appversion="+Ti.App.version+"&manufacturer="+Ti.App.manufacturer+"&model="+Ti.App.model+"&memory="+Ti.Platform.availableMemory;
		url += url.indexOf("?") > 0 ? "&" + append : "?" + append;
	}

	xhr.open(method || 'GET', url);
	if ((method == "POST" || method == "PUT" || method == "DELETE") && args){
		xhr.send(args);
	}
	else{
		xhr.send();
	}
}
```

上面的`Ti.App`是一个命名空间,存储了很多需要调用系统资源的属性，这样就不需要每次都调用系统资源来读取属性了。下面这段代码是指当访问某种特定形式的url时，将App自身的信息也传递到这个接口中去,不考虑信息采集的话这段代码可以加以注释。如下所示:

```javascript
if (url.indexOf(Ti.App.helloworld) == 0){
	var append = "osname="+Ti.App.osname+"&osversion="+Ti.App.osversion+"&appversion="+Ti.App.version+"&manufacturer="+Ti.App.manufacturer+"&model="+Ti.App.model+"&memory="+Ti.Platform.availableMemory;
	url += url.indexOf("?") > 0 ? "&" + append : "?" + append;
}
```


### 有的时候，设置HTTP请求的的header是非常必要的。

在Titanium中设置header的时候，需要主要的是，用来设置header的setRequestHeader()必须要要在open()方法之后，send()方法之前。

```javascript
var client = Ti.Network.createHTTPClient();
client.open("POST", "http://yourservr.com/files/new");
client.setRequestHeader("Content-type", "text/csv");
client.send();
```

## 使用HTTP Client上传(upload)文件

下面以调用本地相册为例，演示如何上传文件:

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

## 下载文件并保存在本地
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

## 可以使用的文件目录

提到将文件保存到本地，就不得不提一下，对于一部手机的OS，都有哪些目录是我们开发者可以使用的。

在Titanium中，主要由四个目录是我们可以使用的：

- Ti.Filesystem.applicationDataDirectory: 可写可读，特定于app，完全卸载或者你手动删除之后，文件消失
- Ti.Filesystem.resourecesDirectory: 只读，完全卸载或者你手动删除之后，文件消失
- Ti.Filesystem.tempDirectory, 可读可写，app完全退出之后，由OS自动将文件内容删除
- Ti.Filesystem.externalStorageDirectory: 可读可写，是外部SD或者类似设备的抽象, 在使用之前，可以使用Ti.Filesystem.isExternalStorageDirectoryPresent()(返回值是Boolean类型)检测设备是否存在。

TODO:结合做的项目的实际代码进行说明。
