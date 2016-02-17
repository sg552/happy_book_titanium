# 如何查看API？

官方文档一般分成两类：

- 教程
- API

教程就是我们平时看到的各种 "tutorial", "guide"。里面都是具体的解说。

API（应用程序接口）则是各种Class/Method的具体定义。
它是软件开发中最重要，也是最乏味的东西。我们离不开它，
但是又不需要掌握所有的内容。

它就跟字典一样：需要的时候用它。厚厚的一大本书，但是我们只为了查找其中的一个字。

看Ti的API，可以去官方站点，也可以下载"Dash", 或者直接下载
"appcelerator Docs". 一般来说，官方站点中的API是最新的。

阅读API是一种非常重要的能力。各种语言的API几乎都一样。 下面我们说明Titanium
的API的使用方法。

![api入口](/images/api_rukou.png)

## Class 的层次
可以看到，左侧的栏目中，从上到下依次是：

- Global: console, JSON, String
- Alloy:  builtins, Collections, Controller, Models, Widget, widgets
等等。

我们可以认为， 小写的都是方法，大写的都是Class

其中，Global 下面的Class，你可以直接拿来用。例如：

```js
console.info();
JSON.stringify();
String.format();
```

其他的类，大部分要完整的加上前面的namespace名。然后按照文档的要求来做. 例如：

```
Alloy.createModel()
Ti.UI.createLabel()
```

builtins 是一个特殊，表示内置方法。例如：

```js
var dialogs = require('alloy/dialogs');
dialogs.confirm();
```

总之，具体如何调用一个方法，务必先看API文档中的例子。

## 每个Class的详情

点击任意一个Class名字，就会出现下图：

![某个Class的详情](/images/api_specific_class_overview.png)

可以看出，每个Class的说明，分为下面几部分：

- properties:  图中有55个.
- methods:  图中有119 个。
- events:  图中有 16 个。
- 父类 ( 例如从 `Titanium.Proxy > Ti.titanium.UI.View` 可以看出, 前者是父类，
所以父类具有的属性和方法，子类都有)
- 对于这个class 用法的描述.
- 该Class适用的不同平台的Ti SDK的起始版本:
  - 在 Ti SDK 0.9 开始支持 安卓, iphone和 ipad
  - 在 Ti SDK 1.8 开始支持移动web
  - 在 Ti SDK 4.1.0 开始支持 windows phone

## properties: 属性

下面是某个Class的属性列表:
![属性列表](/images/api_properties_list.png)

属性列表中，带有 `R O`标志的，意为 "Read Only"，只读。这样的属性，你是无法
为它重新设置值的。

点击某个属性之后，可以看到对这个属性的详细说明：
![属性的详情](/images/api_properties_details.png)

## methods: 方法

下面是某个Class的方法列表：

![方法列表](/images/api_methods_list.png)

可以看出，所有的属性，都有 getter 方法。 所有非 `R O`的属性，都有 setter方法。

由于js语言的特性，访问一个方法时，可以使用getter/setter, 也可以不使用，
例如，下面几行都是等价的：

设置背景色：

```js
view.setBackgroundColor('red');
view.backgroundColor = 'red';
```

获取背景色：

```js
view.getBackgroundColor();
view.backgroundColor;
```

下面是Method的详情：
![方法详情](/images/api_methods_details.png)

可以看出，该方法的作用，返回值，需要的参数等等所有信息，都列出来了。

## events 事件

常见的事件包括了 click, double click, 等等。 无论是在桌面应用程序，还是WEB，
还是手机app中，只要涉及到了用户的操作，就一定会有事件.

事件一般来说是靠两个方法来用：
- addEventListener ， 作为对该事件的捕捉。
- 上面的方法中的第二个参数（我们叫它 callback, 回调函数），
作为对该事件的处理。

例如，下面是个例子：
```js
some_element.addEventListener('click', function(e){
  console.info("我被点击了");
} )
```

几乎所有的语言中，对于事件的用法都是一样的。

以 Ti.UI.View 为例，下面是它的事件列表：

![事件列表](/images/api_events_list.png)

点击任意一个事件，都可以看到详细的情况
![事件详情](/images/api_events_details.png)
- 首先是一段文字说明
- 下面是说明该事件是从Ti SDK的哪个版本开始支持的。(android, ios 都是0.9，
web 是1.8 )
- properties, 事件的属性, 也就是event回调函数中的参数的属性。例如，上图中的
这个 "click"事件，就有若干属性，包括： x, y ...  于是我们就可以这样获取：

```js
some_element.addEventListener('click', function(e){
  console.info("x is: " + e.x);
  console.info("y is: " + e.y);
} )
```

这里很重要，因为对于事件我们用的还是特别多的。

## 如何用好一个Class?

就是多看api, 多翻。

比如下图，好的API都会给出例子（比如下面，比如Rails）

![class的说明](/images/api_readme_example.png)

也有很多api, 只能看到 参数，返回值的说明，没有例子，(十年以前的java API都是
这样)这时候就要结合具体的官方文档或者示例代码去看。

