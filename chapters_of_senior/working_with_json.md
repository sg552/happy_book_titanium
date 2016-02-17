# 操作JSON

每个移动app 都要从服务器端获取json数据，或者发送json到服务器端。

JSON 就是一个Hash. 没什么特殊的。

下面，我们就通过实际的代码来展示，在Titanium中是如何使用JSON的。

首先，跟处理JSON相关的两个function是：

- `JSON.parse()` 将JOSN转化成为Javascript对象，常用于解析http结果。
- `JSON.stringfy()` 将Javascript对象(object)转化成为JSON， 常用于打印日志

```js
var myObject = {
  foo: "bar",
  stuff: [1, 2, 3]
};

// 将Javascript对象转化成为JSON字符串, 返回值是'{"foo": "bar", "stuff": [1, 2, 3]}'
var myObjectString = JSON.stringify(myObject);

// 将JSON转化成为Javascript对象, 返回值是
var myNewObject = JSON.parse(myObjectString)

// 注意，method会被忽略掉
var objectWithMethods = {
  one: function(){console.log("I am a method");},
  two:"i am a text"
};
var oo = JSON.stringify(objectWithMethods);
console.log(oo);
// oo => '{"two":"i am a text"}
```

## 在HTTPClient中处理JSON

主要靠：  `JSON.parse(e.responseText)`

```js
var url = "http://tidev.in/example.json";
var xhr = Ti.Network.HTTPClient();
xhr.onload = function(e) {
	// 解析JSON字符串，变成Javascript对象
	var json = JSON.parse(e.responseText);
  // ...其他代码
};
```

## 最佳实践

- 可以根据 e.status(返回http状态数字)来判断请求是否成功。
- 远程服务器最好永远返回非空的JSON. 例如：

```json
{
  result: []
}
```
而不是：

```json
[]
```

