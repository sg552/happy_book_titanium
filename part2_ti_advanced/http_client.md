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

下面演示如何在手机端发送一个HTTP请求：

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

我们项目中还普遍存在另一种写法，如下：
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

有的时候，设置HTTP请求的的header是非常必要的。

在Titanium中设置header的时候，需要主要的是，用来设置header的setRequestHeader()必须要要在open()方法之后，send()方法之前。

```javascript
var client = Ti.Network.createHTTPClient();
client.open("POST", "http://yourservr.com/files/new");
client.setRequestHeader("Content-type", "text/csv");
client.send();

TODO:结合做的项目的实际代码进行说明。
