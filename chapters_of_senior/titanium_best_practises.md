# Titanium 编码最佳实践 ( coding best practices for Titanium)

2014-11-15 09:18
分类： 技术, 书稿
refer to http://docs.appcelerator.com/titanium/latest/#!/guide/Coding_Best_Practices

JavaScript and general recommendations

1. 避免使用global scope.

1.1 global scope中的 资源(变量啊啥的)无法被 自动回收. 你需要手动的给它变成null

1.2. global scope中的东西容易被覆盖掉.

1.3. global scope中的东西无法被 commonJS 或者其他module 所使用.

什么情况下 变量会被定义在global scope中呢?

a. 在function 或者 commonJS 之外 声明变量

b. 任何不使用var 声明的变量.

2. 不要在 global event listener中使用 local object ,会导致内存泄露.例如:

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
Ti.App, Ti.Geolocation, Ti.Gesture 等关联的event 都是 global event. 所以,尽量不要针对它们使用.

3. event name 不要使用空格. 错误的写法:  'my event' , 正确的写法: 'my:event' or 'my_event'

4. 使用 defer loading (延迟加载)  可以大大加快启动速度.例如:

//muse be loaded at launch
var WindowOne = require('ui/WindowOne').WindowOne;

var win1 = new WindowOne();
win1.open();

win1.addEventListener('click', function() {
  //load window two JavaScript when needed...
  var WindowTwo = require('ui/WindowTwo').WindowTwo;
  var win2 = new WindowTwo();
  win2.open();
  win2.addEventListener('click', function() {
    //load window three JavaScript when needed...
    var WindowThree = require('ui/WindowThree').WindowThree;
    var win3 = new WindowTwo();
    win3.open();
  });
});
下面是针对 Titanium的建议:

5. 不要修改 Titanium的prototype  ( 就是不要使用 Ti 这个namespace .)

6. 对于跨平台的编码, 要么:

  6.1 使用 很多个 if ...else 语句.

  6.2 也可以使用 git branch .

总之各有利弊, 看情况了. 更多看这里:  http://docs.appcelerator.com/titanium/latest/#!/guide/Supporting_Multiple_Platforms_in_a_Single_Codebase

7. 仅仅在 .js 文件中保存敏感信息. 因为 .js 文件在编译(成Titanium能识别的文件) 后, .js 会被压缩, 而且加密(obfusecated ).  如果只是放在了 .txt ,  .sqlite 中,那么这些信息可以直接被 别有用心的人读取到.

8. 尽量少调用 Ti.Platform.osname 这样的方法. 因为会耗费资源.  最好一次读取到本地变量中, 然后多次使用.

9. 使用 CommonJS 来 划分模块.

Do not name custom events with spacesDefer script loadingTitanium-specific RecommendationsDon't Extend Titanium PrototypesCoding strategies for multiplatform appsDon't store sensitive data in non-JavaScript filesSet local variables to avoid calling native methodsApp Architecture RecommendationsModular components with CommonJS

# 来自于实战的经验

1. 先ios 再android
ti 对ios的支持比android的要好一些。所以优先做ios开发。
ios上弄好了之后，再做android开发

2. 使用 console.info 时， 要小心 JSON.stringify() 这个方法很好用，可以打印
出一个json的 所有细节，但是缺点是 当要打印的对象很大时，系统就崩溃了。

3. object-c语言中的JS实现（javascriptCore）与Android中的JS实现（V8）机制
是不同的，一般说来前者更加松散宽容一些。所以一些错误只有到了android中才会
凸显出来。要加强平时的JS修炼

4. 必须了解js中的 异步调用 操作. 这是很多新手犯下的毛病。明明逻辑是对的，
为什么弄起来时好时坏？原因就在于没有用好 异步调用的callback

这里要注意，务必使用 success 这样的事件，绝对不要使用 setTimeout() ，太不合逻辑了。

5. 一些UI做调试时，务必使用好一些属性：borderColor , color 等等。这样的话
可以解决一些莫名其妙的UI问题。

比如，某个ti app中，低版本的android中, 默认字体颜色是白色；高版本的字体
颜色则是黑色。 这时候就要强制加上 `color`属性了。

6. 使用明星框架

代码写在远程，直接导致代码极其容易调试: 不需要编译。 可以随时升级。

7. 使用动态的计算长度标准 __l() 方法。 以往的项目中，我们在调整UI时吃了不少亏。
不同的平台， 同一平台不同的版本，不同尺寸的屏幕，UI都看起来不一样。
这个__l()方法可以永久解决问题。

8. 使用coffeescript 代替 标准javascript.
