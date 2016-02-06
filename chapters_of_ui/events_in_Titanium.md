# Titanium中的各种事件

## 事件

不管是使用原生的Ios,Android 开发出来的应用，还是使用Titanium开发出来的应用，用户总是少不了和手机发生交互，从而触发更多效果。比如点击，滑动，摇一摇，这些行为我们可以称之为事件。

Titanium中提供很多的UI组件是具备很多事件的，例如window,view,listview等，我们可以通过捕获和释放对事件的监听来完成很多操作。

### 常见的一些事件
1.click(点击)

2.dblclick(双击)

3.swipe(左右滑动)

4.scroll(任意方向的滑动)

5.touchstart,touchmove,touchend(touch行为的各种事件)


###  使用例子
```javascript
# 给某个window添加一个点击事件
someWindow.addEventListener('click',function(e){
    Ti.App.info('You clicked me !');
});
```

```javascript
# 给某个window添加一个左右侧滑的监听事件
someWindow.addEventListener('swipe', function(e){
    if (e.direction == 'left') {
    alert('swipe left');
    } else if (e.direction == 'right') {
    alert('swipt right');
    }
});
```

###  关于参数e
使用js来定义一个方法时，很多时候会使用到参数e,如上面两个例子。这里的e就是event。很多时候这个e能给我们提供很多帮助，我们可以选择打印一下这个e。

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

bubbles = 1 ; cancelBubble = 0 ; direction = left ; source = "[object TiUIWindow]" ; type = swipe ; x = 284 ; y = "245.6" ;

我们就着上面这些信息来讲解一部分与事件相关属性：

####事件冒泡（Event Bubbling）
我们使用Titanium开发时，主要使用的就是javascript语言。而这里我们在web端应用的时候，就对事件冒泡（Event Bubbling）有所了解。我们可以这么理解这个概念：
当一个UI组件被点击了，这个UI组件就是此次点击事件的目标。如果已经给这个UI组件对象定义好了事件处理程序，则事件会调用对应的事件处理程序。但如果没有定义任何处理程序，抑或定义的处理程序的返回值为‘true’，这个事件会向这个UI组件对象的父类UI容器传播，这就像冒泡一样。

我们看到上面的打印信息中有两条这样：bubbles = 1 ; cancelBubble = 0; 这两句的意思就是把允许事件冒泡传递给它对应的父级UI。

#####注意：
1.有些特殊的容器，比如window，在UI层次中就没有父级UI容器。所以，当事件冒泡传递到一个特殊的UI容器时就会停止结束传递。这些特殊的UI容器有如下：
+ Window
+ NavigationWindow
+ SplitWindow
+ Tab
+ TabGroup

2.并不是所有的事件都会能冒泡（bubble），一些特殊的事件例如：focus ，scroll就不具有事件冒泡。如下这些事件就具备事件冒泡行为：
+ click
+ dblclick
+ longclick
+ singletap
+ doubletap
+ longpress
+ pinch
+ swipe
+ touchcancel
+ touchend
+ touchmove
+ touchstart
+ twofingertap

####事件源（Event Source）
Source就是事件触发的源头，点击某个button，该button就是这次事件的源，点击某个view，该view就是这次事件的源。以上的例子中我们写的并不突出，我们看看下面这个例子。


```javascript
var view = Ti.UI.createView({
    backgroundColor:'red',
    width: '100',
    height: '200'
});

view.addEventListener('touchmove', function(e)
    {
    Ti.API.info(e.source.width) //打印该view的宽
    Ti.API.info(e.source.height) //打印该view的高
    });

```
编程时，利用好这个e.source能给我们的调试和开发带来极大的方便。

####事件的其他属性
上面的例子中，我们还看到了事件的类型type是swipe，事件的方向direction是left，还有对应的x，y坐标值。

####ListView中event
我们知道在使用ListView的时候，要定义ItemTemplate，这里面就会用到一个属性叫bindId，我们可以通过查看或者判断bindId来定位到你所点击的对象。此外，我们还可以使用e.itemIndex来确定ListView的列表的各个index。


###  不同平台的特殊事件
Titanium号称跨平台，可是现实中安卓和苹果长得一点也不像，而且事实Titanium对Ios的支持实在是太偏爱了，但也不是说对安卓就支持不够，它还是根据不同的平台提供不同的支持。就比如安卓提供很多物理按键。比如返回，主页，搜索按钮，而对于这些特殊的安卓的功能，Titanium也提供特殊的事件来响应。如下：

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
等等一些事件。


### Alloy中事件的使用
很多情况下我们开发的时候都是借助Titanium官方提供的MVC框架Alloy。既然是MVC框架，它就会有视图层，控制层，模型层。使用Alloy时，给UI添加事件监听事件既可以在控制层，也可以在视图层，但显然定义只能写在控制层，如下：

```javascript
# index.js
function open_win2(e) {
    var win2 = Titanium.UI.createWindow({
    title: 'win2',
    backgroundColor: 'white',
    class: 'container'
});

var back_button = Titanium.UI.createButton({
    title:'back'
});

back_button.addEventListener('click', function(){
    win2.close({animated:true});
    });

win2.add(back_button);
win2.open();
}
```

```xml
<!---index.xml--->
<Alloy>
  <Window>
    <Button title = 'open win2' onClick = 'open_win2' />
  </Window>
</Alloy>
```
从上面的例子我们可以看到，事件的处理程序的定义一定要写在控制层，但是事件的绑定可以写在视图层，也可以写在控制层。值得注意的是，当你帮事件的绑定写在视图层的时候，要注意事件的特殊性，并不是所有的点击事件都写‘onClick = ’,比如在ListView中item点击事件，写在xml文件的时候，是写成‘onItemclick= ’，否则对应不上。这是要注意的地方。

### 事件的使用
#### 触发事件

```javascript
button.fireEvent('click');//直接触发点击事件
```
使用这个方法的时候，还可以传递数据
```javascript
button.fireEvent('click',{width: '100'});//这个传递的参数可写可不写
```

#### 绑定事件
```javascript
element.addEventListener('event_type', function(e) {
    // 这里写你的方法体
    // 这里的方法会在事件被触发的时候执行
    Ti.API.info('The '+e.type+' event happened');
    });
```

#### 移除事件
```javascript
function doSomething(e) {
  //你的方法
  }

deleteButton.addEventListener('click', doSomething);

//或者

deleteButton.removeEventListener('click', doSomething);
});
```
