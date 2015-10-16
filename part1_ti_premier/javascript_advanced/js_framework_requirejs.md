# export
refer to http://requirejs.org/docs/start.html

RequireJS是一个javascript文件，是一个module加载器，主要用于浏览器内部的优化，但是也可以用于其他的环境，比如：`Rhino`,`Node`。使用RequireJS能够提高代码质量。

在写titanium应用时，为了提高代码质量，经常需要将功能提取出来做成相应的CommonJS的module，然后使用RequireJS的module加载功能直接加载module。

```javascript
//label_window.js

function label_win (args){
  self = Ti.UI.createWindow(
    backgroundColor: 'white',
    hideNavBar: true,
    title: args.title
  );

  var lb = Ti.UI.createLabel({
    text: args.text,
    borderRadius: 5,
    backgroundColor: 'pink'
  });
  self.add(lb);

  return self;
}

module.exports = label_win;
```

```javascript
//index.js

var label = require('label_window');
var args = {
  title: 'label window',
  text: 'this is a new window with a label'
}
var lb = new label(args);
lb.open();
```

在CommonJS module中通常使用`module.exports`和`exports`两种导出方式。

使用`exports`方式
```javascript
//hello.js
var a = "hello";
var b = function (){
  console.info(a);
}
exports.a = a;
exports.b = b;
```

```javascript
//prints.js
var print = require('./hello.js');
print.b();   // => hello
```
使用`module.exports`方式
```javascript
//hello.js
var a = "hello";
var b = function (){
  console.info(a);
}
module.exports = b;
```

```javascript
//prints.js
var print = require('./hello.js');
print();   // => hello
```

当`exports`没有被赋值时可以看做是指向`module.exports`的，两种方式返回的结果一样，当`exports`赋值后，改变了其原来的指向，和`module.exports`结果不同。使用`exports`方法返回的是一个`object`类型方法，使用`module.exports`方法返回的是一个`class`方法，所以`module.exports`可以使用new方法，如
```javascript
var fruit = require('fruit');
var apple = new fruit();
```

建议使用`module.exports`
