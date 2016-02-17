# 编码最佳实践 ( coding best practices for Titanium)

## 对于全局范围内的建议 (Global Scope)

  - global scope中的 资源(变量啊啥的)无法被 自动回收. 你需要手动的给它变成null
  - global scope中的东西容易被覆盖掉.
  - global scope中的东西无法被 commonJS 或者其他module 所使用.

什么情况下 变量会被定义在global scope中呢?

- 在function 或者 commonJS 之外 声明变量
- 任何不使用var 声明的变量.
- 不要在 global event listener中使用 local object ,会导致内存泄露.例如:

```js
var someFunction = function() {
  var table = Ti.UI.createTableView(),
      label = Ti.UI.createLabel(),
      view = Ti.UI.createView();

  Ti.App.addEventListener('bad:move', function(e) {
      table.setData(e.data);
  });

  view.add(table);
  view.add(label);

  return view;
};
```
Ti.App, Ti.Geolocation, Ti.Gesture 等关联的事件都是 global 事件.
所以,尽量不要针对它们使用.

- event name 不要使用空格.
  - 错误的写法:  'my event' ,
  - 正确的写法: 'my:event',  'my_event'

## 对于使用Titanium的建议

不要修改 Titanium的prototype  ( 就是不要使用 Ti 这个namespace .)

## 对于跨平台的编码

把代码写在一起。使用if ..else 来判断不同的平台。例如：

```js
if(Ti.OS.android) {
  // 针对android的代码
}
else if(Ti.OS.ios) {
  // 针对ios的代码
}
```
绝对不要使用多个branch来分别管理不同的平台。那样的话Titanium就失去意义了。

## 处理敏感信息

仅仅在 .js 文件中保存敏感信息. 因为 .js 文件在编译(成Titanium能识别的文件) 后,
 .js 会被压缩, 而且加密(obfusecated ).

如果只是放在了 .txt ,  .sqlite 中,那么这些信息可以直接被 别有用心的人读取到.

## 把耗时的操作的结果，放到系统常量中

- 尽量少调用 Ti.Platform.osname 这样的方法. 因为会耗费资源.
最好一次读取到本地变量中(例如 Ti.App 变量中), 然后多次使用.

- 使用 CommonJS 来 划分模块.

# 来自于实战的经验

## 两个一起弄，或者先做ios 再做android

- 在大的时间尺度上，是两个平台一起弄。
- 小的时间尺度上，先做ios,
因为ti 对ios的支持比android的要好一些，编译速度快，时间短，在5.1.1之前，
修改app.js 直接退出app 重新进即可。都不需要编译的。

## 针对大对象，慎用 `JSON.stringify`

使用 console.info 时， 要小心 JSON.stringify() 这个方法。它很好用，可以打印
出一个json的 所有细节，但是缺点是 当要打印的对象很大时，系统就崩溃了。

## 不同平台的js 实现机制不同

Object-C语言中的JS实现（JavascriptCore）与Android中的JS实现（V8）机制
是不同的，一般说来前者更加松散宽容一些。所以一些错误只有到了android中才会
凸显出来。要加强平时的JS修炼

## 掌握异步调用的机制

必须了解js中的 异步调用 操作. 这是很多新手犯下的毛病。明明逻辑是对的，
为什么弄起来时好时坏？原因就在于没有用好 异步调用的callback

这里要注意，务必使用 success 这样回调函数，绝对不要使用 setTimeout() ，
太不合逻辑了。

## 调试UI时，用好属性

一些UI做调试时，务必使用好一些属性：borderColor , color 等等。
这样的话可以解决一些莫名其妙的UI问题。

比如，某个ti app中，低版本的android中, 默认字体颜色是白色；高版本的字体
颜色则是黑色。 这时候就要强制加上 `color`属性了。

## 使用明星框架

代码写在远程，直接导致代码极其容易调试: 不需要编译。 可以随时升级。

## 使用动态的计算长度标准

也就是明星框架中的 `__l()` 方法。 以往的项目中，我们在调整UI时吃了不少亏。
不同的平台， 同一平台不同的版本，不同尺寸的屏幕，UI都看起来不一样。
这个__l()方法可以永久解决问题。

## 使用coffeescript + grunt watch

- coffeescript: 大大简化代码
- grunt watch: 大大简化编译coffee的时间
