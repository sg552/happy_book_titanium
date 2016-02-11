# Scrollable View

大部分的app的首页，都会有轮播图。好的轮播图会让app看起来新奇有意思。

ScrollableView就是用来实现图片的轮播和复杂的图片滑动布局。

注意： ScrollView 是滚动图，不是轮播图。

![scrollable view](/images/ui_scrollable_view.gif)

```js
var win = Ti.UI.createWindow({backgroundColor: 'white'});

v1 = Ti.UI.createView({
  backgroundColor: 'red'
});
v2 = Ti.UI.createView({
  backgroundColor: 'blue'
});
v3 = Ti.UI.createView({
  backgroundColor: 'green'
});

var scrollable_view = Ti.UI.createScrollableView({
  views: [v1, v2, v3],
  showPagingControl: true
});
win.add(scrollable_view);
win.open();
```

## 控制在安卓上和iOS上的样式

TODO: 明星补充
