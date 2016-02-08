# 使用requirejs 把titanium代码理清楚

## requirejs 介绍
RequireJS是一个javascript文件，是一个module加载器，主要用于浏览器内部的优化，
但是也可以用于其他的环境，比如：`Rhino`,`Node`。它能让代码模块化，使用它
可以提高代码质量。

在写titanium应用时，为了提高代码质量，经常需要将功能提取出来做成相应的
CommonJS的module，然后使用RequireJS的module加载功能直接加载module。

例如： 这个文件，是：label_window.js

```javascript
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

我们就可以在另一个文件中调用：index.js
```javascript

var label = require('label_window');
var args = {
  title: 'label window',
  text: 'this is a new window with a label'
}

new label(args).open();
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


## titanium 中使用require 来引用js module

两种方法都可以，注意不要弄混。

### 使用 module.exports

1. 需要你的js module文件放到 Resources 目录下：

看起来这样：

```js
// Resources/utils.js
function say_hi(){
     console.info("=== hihihi ");
}

module.exports = say_hi;
```

2. 在 app.js 或者其他文件中：

```js
var hi_module = require('utils');
temp = new hi_module();
```
就可以了。

启动Ti时，在控制台上就可以看到：

```
[DEBUG] Module: Loading module: util -> Resources/util.js
[INFO]  ==== after require, before new ..
[INFO]  == hihihi
```

### 也可以使用`exports.xxyy`的形式

例如：

```js
logger = require('logger')
logger.info(' some info...');
logger.debug(' some debug message...');
```
那么，该logger.js的文件应该是：

```js
function info(message){
    console.info(message)
}
function debug(message){
    console.info(debug)
}
exports.info = info
exports.debug = debug
```

## required项目中的文件路径问题

在Ti中， require的根目录在Resources目录下

如果有个文件：  `Resources/logger.js`, 那么下面两种方法都对：

```js
require ('logger');

require ('/logger');
```

如果有两个文件：

`Resources/dir1/file1` ,  `Resources/dir1/file2`,
那么，在 file2中可以直接  `require('file1')`。 但是尽量使用完整的名字吧，
看起来清晰些。
