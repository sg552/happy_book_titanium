# Widgets

Widgets 是 Alloy 框架的一部分重要功能, 封装好的 Widgets 能够被重用。

## 如何使用

在开始生成一个新的项目的时候 Titanium 会自动帮我们创建一个 `app/views`
`app/controllers` `app/styles` 文件夹，用于存储 `MVC` 框架对应的文件。
Widgets 是属于 Alloy 框架的内容，因此我们需要在 `app` 目录下手动创建
`app/widgets` 目录,总共分为三个步骤:

 复制 `com.example.widget(widget名字)` 到新创建的 app/widgets 目录下面。如下图所示:

```
app
├── config.json
├── controllers
│   └── index.js
├── views
│   └── index.xml
└── widgets
    └── com.example.widget
      ├── controllers
          │   ├── foo.js
          │   └── widget.js
          ├── views
          │   ├── foo.xml
          │   └── widget.xml
          └── widget.json
```
 在 `app/config.json` 文件里面的 `dependencies` 属性里面声明 `widget` 的 `name` 和 `version` 的键值对:

```javascript
{
    ...
      "dependencies": {
        "com.example.widget":"1.0"
    }
}
```
 在需要引用 `widgets` 的地方调用 `com.example.widget` 。

在 View 中调用：

app/views/index.xml
```xml
<Alloy>
      <Window>
          <Widget src="com.example.widget" id="foo" name="foo" />
      </Window>
</Alloy>
```

也可以在 controller 中调用：

```javascript
widget = Alloy.createWidget('com.example.widget');
```

重新编译项目，这时候的widgets便被成功使用了。


## 如何创建一个widget

Widgets 作为组件在程序启动时自动加载，内置 view , style , controller ,
models , theme , assets , libs 等等。因此，view 视图, controller 里面的
`function` , style 里面的 tss 样式等都能够被重复使用。

以下例子引用的官方的alloy/test/apps/widgets/wpath/widgets 的示例,
创建下面的目录和文件结构:

```
app
├── config.json
├── controllers
│   └── index.js
├── views
│   └── index.xml
└── widgets
    └── com.test.hellobutton
      ├── assets
      │   └── hello.png
      ├── controllers
          │   └── widget.js
          ├── lib
          │   └── hello.js
          ├── styles
          │   └── widget.tss
          ├── views
          │   └── widget.xml
          └── widget.json
```
controller文件里面定义了一个方法，并且require了一个本身的lib/hello.js 文件，看到加上了WPATH标签,指的是引用当前widget目录下的lib文件。

widget.js

```javascript
function sayHello() {
  // the path in manually, it would look like this:
  //
  //     require('com.test.mywidget/hello').sayHello();
  require(WPATH('hello')).sayHello();
}
```

注意这里的WPATH指的是 `widget/assets` 目录下,不是 `app/assets`下面的图片。

widget.tss

```css
"#helloButton": {
    backgroundImage: WPATH('hello.png'),
    height: 135,
    width: 233
}
```

widget.xml

```xml
<Alloy>
  <Button id="helloButton" onClick="sayHello"/>
</Alloy>
```

`exports.<method name>`,声明该方法,试该方法能够被外部调用。

hello.js

```javascript
exports.sayHello = function() {
    alert('Hello!');
};
```

widget.json: 按照下面的格式，输入必要的信息即可。这个文件在功能上不重要。

```json
{
  "id": "com.test.hellobutton",
  "name": "Hello Button",
  "description" : "A button, that when pressed, says hello",
  "author": "Jim",
  "version": "1.0",
  "min-alloy-version": "0.2.35",
  "min-titanium-version":"2.1",
  "tags":"",
  "platforms":"android,ios,mobileweb,windows",
  "dependencies": {}
}
```

widget创建结束，这时候可以用前面提到的方法来使用该widget了。

## 资源

Titanium 官方提供一些 Widgets

http://gitt.io 有许多不错的 Wigets 和 modules

