Hello, HTTPClient!

Titanium实现了五个HTTP的方法，分别是GET, POST, PUT, DELETE, PATCH

常用的就两个GET和POST。

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

TODO:结合做的项目的实际代码进行说明。
