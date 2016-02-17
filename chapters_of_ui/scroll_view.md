# ScrollView

ScrollView是一种类似于TableView和ListView的一种视图布局，它和ListView和
TableView的区别是: 使用它可以实现Scrollview内部的子控件横向和纵向的
滑动。

实际应用中有一点的瑕疵，Scrollview中的子控件如果是ImageView(实现图片下滑)，
则最后一张图片不会被完全滑动上去。

我们的解决方案是在最后面加上一个空的label, 来hack这个简单的bug。

（注意下图中的图片在滚动过程中产生的 滚动条)

![scrollview](/images/ui_scrollview.gif)

```js
var scrollView = Ti.UI.createScrollView({
  showVerticalScrollIndicator: true,
  showHorizontalScrollIndicator: true,
  height: '80%',
  width: '80%'
});

var win = Ti.UI.createWindow({
  backgroundColor: 'white',
  exitOnClose: true,
  fullscreen: false,
  title: 'ScrollView Demo'
});


var view = Ti.UI.createView({
  backgroundColor:'#336699',
  borderRadius: 10,
  top: 10,
  height: 2000,
  width: 1000
});

scrollView.add(view);
win.add(scrollView);
win.open();
```
