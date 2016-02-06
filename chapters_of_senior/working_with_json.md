#JSON

#简介
是实际的Titanium开发中，经常要从server端获取json，或者发送json到server端。

下面，我们就通过实际的代码来展示，在Titanium中是如何使用JSON的。

首先，跟处理JSON相关的两个function是：

- `JSON.stringfy()` 将Javascript对象(object)转化成为JSON
- `JSON.parse()` 将JOSN转化成为Javascript对象

```javascript
var myObject = {foo: "bar", stuff: [1, 2, 3]};
// 将Javascript对象转化成为JSON字符串, 返回值是'{"foo": "bar", "stuff": [1, 2, 3]}'
var myObjectString = JSON.stringify(myObject);
// 将JSON转化成为Javascript对象, 返回值是
var myNewObject = JSON.parse(myObjectString)

// 注意，method会被忽略掉
var objectWithMethods = {one: function(){console.log("I am a method");}, two:"i am a text"};
var oo = JSON.stringify(objectWithMethods);
console.log(oo); 
// oo => '{"two":"i am a text"}
```

## 使用Titanium处理JSON

#### 接收JSON数据
```javascript
var url = "http://example.com/json.txt";
var xhr = Ti.Network.HTTPClient();
xhr.onload = function() {
	// 解析JSON字符串，变成Javascript对象
	var json = JSON.parse(this.responseText);
	// 使用json的代码
	// do something or some methods
};
xhr.error = function() {
// 用来处理错误的代码
};
```


### 发送JSON数据

发送JSON，还是要使用HTTPClient。

send()方法可以接受null, dictionary, string, File object, Blob data这些参数。

send()会自动将要发送的数据stringify，所以不用显示的调用JSON.stringify()，除非你使用GET方法发送JSON数据。
```javascript
var blogPost = {title: "this is the title", body: "This is the body"};
var xhr = Ti.Network.HTTPClient();
xhr.onload = function() {
  // 处理响应
}；
xhr.open("POST", "http://www.myblog.com/interface/post/new");
xhr.send(blogPost);
```

TODO: 将获取的数据使用在tableView或者listView中，结合实际的项目
