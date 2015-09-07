# Titanium.UI.ScrollView
ScrollView在实战中通常可以实现图片的轮播，和复杂的图片滑动布局。
ScrollView是一种类似于TableView和ListView的一种视图布局，它和ListView和
TableView的区别是使用它可以实现scrollview内部的子控件可以横向和纵向的
滑动，在实际应用中也有那么一点的瑕疵，例如scrollview中的子控件是ImageView
实现图片下滑，那么会有一个不起眼的bug，就是最后一张图片不会被完全滑动上去。
那么我们的解决方案是在最后面加上一个空的label,来解决这个简单的bug。


在controller中创建ScrollView的例子:

*app/controllers/index.js*

```javascript

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





在View中创建ScrollView的例子:

*app/views/index.xml*

```xml

<Alloy>
   <Window id="win" backgroundColor="white" exitOnClose="true" fullscreen="false" title="ScrollView Demo">
     <ScrollView id="scrollView" showVerticalScrollIndicator="true" showHorizontalScrollIndicator="true" height="80%" width="80%">
        <View id="view" backgroundColor="#336699" borderRadius="10" top="10" height="2000" width="1000" />
     </ScrollView>
   </Window>
</Alloy>

```

