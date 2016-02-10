# ActivityIndicator

很多时候，App的操作是需要用户等待的：访问远程资源，某些耗时的操作等等。
这时务必要告诉用户，否则用户会以为：是不是你的app出问题了？

ActivityIndicator 就是为了这个目的而产生的。

![android](/images/activityindicator_android.png) | ![ios](/images/activityindicator_ios.png) | ![Windows Phone](/images/activityindicator_windowsphone.png)
:---:|:---:|:---:
安卓 | ios | Windows Phone


## 注意

1. 和别的view一样，ActivityIndicator在它显示之前也是需要被添加到一个window
容器或者其他别的顶级容器中的。和其他view不一样的是：默认的情况下，
它预先是被隐藏的，只用你调用它的`show()`方法的时候，它才会显示。

2. 早于SDK 3.0之前，Android的ActivityIndicator会生成一个对话框，
里面有spinner或者进度条。而SDK 3.0 之后，原先Andorid的这种ActivityIndicator
的效果被重新命名叫做`Titanium.UI.Andorid.ProgressIndicator`。


## 例子

```js
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
  font: {
    fontFamily:'Helvetica Neue', fontSize:26, fontWeight:'bold'
  },
  message: 'Loading...',
  style:style,
  top:10,
  left:10,
  height:Ti.UI.SIZE,
  width:Ti.UI.SIZE
});

// activity indicatory 一定要被加进某个window或者别的顶级view中来显示它
win2.add(activityIndicator);

win2.addEventListener('open', function (e) {
  activityIndicator.show();

  // 6 秒钟之后就关闭
  setTimeout(function(){
    e.source.close();
    activityIndicator.hide();
  }, 6000);
});

win1.open();
win2.open();
```

