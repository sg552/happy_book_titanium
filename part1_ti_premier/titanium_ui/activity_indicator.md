#ActivityIndicator
用户在使用应用的时候，经常需要在数据请求，或者初始化的时候等待，如果这个时候，应用不提供一些UI效果让用户打发一下时间的话，仅仅是让客户看着空白的屏幕发呆，我想这样的用户体验是非常不好的。所以，Titanium也提供了这样的东西就叫ActivityIndicator。

ActivityIndicator是为了通过一个UI效果给用户告知当前程序正在执行一个不知道进度的行为操作着，如果想要知道当前的进度(例如请求远程数据，初始化数据)应该使用`Titanium.UI.ProgressBar`。
##使用方法
+ 1.在javascript代码中通过方法`Titanium.UI.createActivityIndicator`来实例化一个ActivityIndicator对象。
+ 2.如果使用Alloy框架，也可以在xml文件中使用`<ActivityIndicator>`标签来创建一个ActivityIndicator对象。

###注意
+ 1.和别的view一样，ActivityIndicator在它显示之前也是需要被添加到一个window容器或者其他别的顶级容器中的。和其他view不一样的是：默认的情况下，它预先是被隐藏的，只用你调用它的`show()`方法的时候，它才会显示。
+ 2.早于SDK 3.0之前，Android的ActivityIndicator是会生成一个对话框，里面有spinner或者进度条。而SDK 3.0 之后，原先Andorid的这种ActivityIndicator的效果被重新命名叫做`Titanium.UI.Andorid.ProgressIndicator`。

##例子
###完全在javascript文件中实现(参考来自官方文档中的例子)
```javascript
Ti.UI.backgroundColor = 'white';

//创建一个最底层的window，背景颜色为蓝色
var win1 = Ti.UI.createWindow({
  backgroundColor: 'blue'
});

//创建一个用来显示ActivityIndicator的window，背景颜色为黄色
var win2 = Ti.UI.createWindow({
  backgroundColor: 'yellow',
  fullscreen: true
});

//这里要注意的是：不同platform的ActivityIndicator的style都是不一样的。
//所以这里要分平台讨论，不能公用，下节会讲到这个问题。
var style;
if (Ti.Platform.name === 'iPhone OS'){
  style = Ti.UI.iPhone.ActivityIndicatorStyle.DARK;
}
else {
  style = Ti.UI.ActivityIndicatorStyle.DARK;
}

//实例化一个对象，并且设定一些属性的值
var activityIndicator = Ti.UI.createActivityIndicator({
  color: 'green',
  font: {fontFamily:'Helvetica Neue', fontSize:26, fontWeight:'bold'},
  message: 'Loading...',
  style:style,
  top:10,
  left:10,
  height:Ti.UI.SIZE,
  width:Ti.UI.SIZE
});

// activity indicatory一定要被加进某个window或者别的顶级view中来显示它
win2.add(activityIndicator);

//监听事件一定要在被触发之前被加载
//`open()`方法一定要定义在被调用之前
win2.addEventListener('open', function (e) {
    activityIndicator.show();
    // 这里你可以写上你的代码，下面是让它显示6秒之后就关闭`hide()`
    setTimeout(function(){
      e.source.close();
      activityIndicator.hide();
      }, 6000);
    });

win1.open();
win2.open();
```

###在Alloy框架中实现以上相同效果
win1.xml:
```xml
<Alloy>
    <Window onOpen="openWin2" backgroundColor="blue" />
</Alloy>
```
win1.js:
```javascript
function openWin2 () {
    var win2 = Alloy.createController('win2').getView();
    win2.open();
}
```
win2.xml:
```xml
<Alloy>
    <Window onOpen="showIndicator" fullscreen="true" backgroundColor="yellow">

        <!-- 对应的样式设置写在 TSS 文件-->
        <ActivityIndicator id="activityIndicator" message="Loading..."/>
    </Window>
</Alloy>
```
win2.js:
```javascript
function showIndicator(e){
  $.activityIndicator.show();
  // 这里你可以写上你的代码，下面是让它显示6秒之后就关闭`hide()`
  setTimeout(function(){
      e.source.close();
      $.activityIndicator.hide();
      }, 6000);
}
```
