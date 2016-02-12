# 事件和处理

事件和对事件的处理，是所有系统中都会用到的技术，一通百通。记住:

- 声明(接收)事件就用 `element.addEventListener`,
- 处理事件，就在listener 中声明对应的方法。
- 触发事件，用 `fireEvent`。 可以加参数。

## 事件

不管是使用原生的Ios,Android 开发出来的应用，还是使用Titanium开发出来的应用，
用户总是少不了和手机发生交互，从而触发更多效果。比如点击，滑动，摇一摇，
这些行为我们可以称之为事件。

Titanium中提供很多的UI组件是具备很多事件的，例如window,view,listview等，
我们可以通过捕获和释放对事件的监听来完成很多操作。

事件有系统自带的，也有我们自定义的。

下面是常见的几个事件：

- click(点击)
- dblclick(双击)
- swipe(左右滑动)
- scroll(任意方向的滑动)
- touchstart,touchmove,touchend(touch行为的各种事件)


###  例子
```js
// 给某个window添加点击事件
some_window.addEventListener('click',function(e){
    Ti.App.info('你点击了我');
});
```

```js
// 给某个window添加一个左右侧滑的监听事件
someWindow.addEventListener('swipe', function(e){
  if (e.direction == 'left') {
    alert('swipe left');
  } else if (e.direction == 'right') {
    alert('swipt right');
  }
});
```

###  关于参数e

使用js来定义一个方法时，很多时候会使用到参数e,如上面两个例子。
这里的e就是event。很多时候这个e能给我们提供很多帮助，
我们可以选择打印一下这个e。

```javascript
# 在上面某个window的swipe事件中打印e的信息
someWindow.addEventListener('swipe', function(e){
  if (e.direction == 'left') {
    alert(e);
  } else if (e.direction == 'right') {
    alert(e);
  }
});
```

我们运行上面代码块时，会在alert中显示触发这个方法时，event的所有信息:

```
bubbles = 1 ; cancelBubble = 0 ; direction = left ;
source = "[object TiUIWindow]" ; type = swipe ; x = 284 ; y = "245.6" ;
```

实际上这个e是个hash, 里面包含了所有的信息。

我们就着上面这些信息来讲解一部分与事件相关属性：

### 事件冒泡（Event Bubbling）

UI组件，如果把一个window 上放一个Label, 当我点击Label的时候，其实也点击到了
window上。

这时就有两个选择：

- label 响应完我的点击，事件就结束了。
- label 响应完我的点击后，window 继续响应。因为我的手指戳在了Label上，也就是
戳在了window上。

也就是，第一种情况时，事件没有从子元素冒泡到父元素，第二种则有。

回到上面的打印信息，信息中有两条这样：`bubbles = 1 ; cancelBubble = 0;`
这两句的意思就是把允许事件冒泡传递给它对应的父级UI。

注意：
1.有些特殊的容器，比如window，在UI层次中就没有父级UI容器。
所以，当事件冒泡传递到一个特殊的UI容器时就会停止结束传递。
这些特殊的UI容器有如下：

- Window
- NavigationWindow
- SplitWindow
- Tab
- TabGroup

2.并不是所有的事件都会能冒泡（bubble），一些特殊的事件例如：focus ，
scroll就不具有事件冒泡。如下这些事件就具备事件冒泡行为：

- click
- dblclick
- longclick
- singletap
- doubletap
- longpress
- pinch
- swipe
- touchcancel
- touchend
- touchmove
- touchstart
- twofingertap

### 事件源（Event Source）

Source就是事件触发的源头，点击某个button，该button就是这次事件的源，
点击某个view，该view就是这次事件的源。

看看下面这个例子:

```javascript
var view = Ti.UI.createView({
  backgroundColor:'red',
  width: '100',
  height: '200'
});

// 这里的e.source 就是被点击的元素
view.addEventListener('touchmove', function(e) {
  Ti.API.info(e.source.width) //打印该view的宽
  Ti.API.info(e.source.height) //打印该view的高
});

```

编程时，利用好这个e.source能给我们的调试和开发带来极大的方便。

### 事件的其他属性

上面的例子中，我们还看到了事件的类型type是swipe，事件的方向direction是left，
还有对应的x，y坐标值。

### ListView中event

在使用ListView的时候，要定义ItemTemplate，这里面就会用到一个属性叫bindId，
我们可以通过查看或者判断bindId来定位到你所点击的对象。

此外，我们还可以使用e.itemIndex来确定ListView的列表的各个index。

###  不同平台的特殊事件

Titanium号称跨平台，可是现实中安卓和苹果长得一点也不像，而且事实上
它还是根据不同的平台提供不同的支持。就比如安卓提供很多物理按键, 比如返回，
主页，搜索按钮，而对于这些特殊的安卓的功能，Titanium也提供特殊的事件来响应。

如下：

平台| 事件 | 使用方法
---| --- | ---
Android | androidback | 在安卓的物理返回键被按下时触发
Android | androidhome | 在安卓的物理主页键被按下时触发
Android | androidsearch | 在安卓的物理搜索键被按下时触发
Android | androidcamera | 在安卓的物理相机键被按下时触发
Android | androidfocus | 在安卓的物理相机键被按下一半时触发
Android | androidvolup | 在安卓的物理音量放大键被按下时触发
Android | androidvoldown | 在安卓的物理音量减小键被按下时触发
Ios | pinch | 两指缩放操作
Ios | delete | Listview中允许用户随意删除一行数据
Ios | move | Listview中允许用户随意拖动一行数据摆放

## 事件的使用

### 触发事件

普通用法：
```js
//直接触发点击事件
button.fireEvent('click');
```

还可以传递数据:
```javascript
//传递的参数是一个Hash
button.fireEvent('click',{width: '100'});
```

### 绑定事件
```js
element.addEventListener('event_type', function(e) {
  // 这里写你的方法体
  // 这里的方法会在事件被触发的时候执行
  Ti.API.info('The '+e.type+' event happened');
});
```

### 移除事件

如果要移除某个定义好的事件，务必这个方法要有个名字，不能是匿名函数：

```js
function do_something(e) {
  //你的方法
}

button.addEventListener('click', do_something);

//或者
button.removeEventListener('click', do_something);
```
