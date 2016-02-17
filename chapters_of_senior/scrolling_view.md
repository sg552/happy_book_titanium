# ScrollView 与 ScrollableView

Titanium提供两种可以滑动的view，`ScrollView`和`ScrollableView`。
虽然名字很像很接近，但是功能上确是有很多的不同。

可以先看看下面两张图片大概区别下：
![](http://image.tidev.in/image/168/Screen_shot_2011-12-08_at_11.42.09_AM.png)

从上面可以看出：

- ScrollView是一个可滑动的内容容器，它不需要全部充满整个视图窗口。
用户可以用手指任意方向的拖动来实现滑动。

- ScrollableView是一个可以容纳多个子view的全屏控件。
类似于coverflow view 或者类似于水平滑动来切换图片的相册。
通常，ScrollabelView都会带一个page indicator（滚动条）。
ScrollabelView只能水平的滑动！

## ScrollView

你可以用`Ti.UI.createScrollView()`方法来创建ScrollView，如下：

```javascript
var sv = Ti.UI.createScrollView({
  height: 200,
  width: 200,
  contentHeight: Ti.UI.SIZE,
  contentWidth: Ti.UI.SIZE
})
```
`height`和`width`定义了ScrollView在window中要占据多大的空间 。
`contentHeight`和`contentWidth`定义了内容区域在ScrollView中占据的区域大小。
默认这是用来设置内容的大小的。

### ScrollView的属性

Property | Description
--- | ---
zoomScale, minZoomScale, maxZoomScale (缩放) | 用来缩放。
horizontalBounce, verticalBounce (反弹动画效果) | (仅用于iOS ) 设置当手指划到顶部时，屏幕的动画是否有反弹效果.
showHorizontalScrollIndicator, showVerticalScrollIndicator (滚动条) | 是否显示滚动条.
scrollType (滚动类型) | 在Android上, 可以选择是竖直还是水平的.
canCancelEvents | ios 上，可以设置成true, 事件就只被ScrollView处理了.

### Android上的要注意的问题

在Android上，可以水平滑动也可以垂直滑动，但不会同时支持两个方向。如果你没有设定指定的scrollType的话，具体能怎么滑动就的依据下面这两条逻辑来看了：

- 设置了width和contentWidth，相当于把ScrollType设置为`vertical`
- 设置了height和contentHeight，相当于把ScrollType设置为`horizontal`

### ScrollView 的事件

## ScrollabelView

scrollableView是用来显示一群`Ti.UI.VIEW`的对象的可滑动容器。
你可以先于scrollableView之前创建它的子view，也可以在之后创建。如下：

```javascript
var view1 = Titanium.UI.createView({backgroundColor:'#123'});
var view2 = Titanium.UI.createView({backgroundColor:'#234'});
var view3 = Titanium.UI.createView({backgroundColor:'#345'});
var scrollable = Titanium.UI.createScrollableView({
	views:[view1,view2,view3],
  	showPagingControl: true
});
win.add(scrollable);
// 再增加一个view
var view4 = Titanium.UI.createView({backgroundColor:'#456'});
scrollable.addView(view4);
// 再删掉一个view
scrollable.removeView(view1);
```

通常你应该先创建view们，然后再把它们以数组的形式添加到ScrollableView中。
理论上，这种方法渲染视图最快。

### ScrollableView 的属性

Property | Description
--- | ---
showPagingControl | 是否显示轮播图下的几个小点儿。
pagingControlColor | 更改轮播图小点儿的颜色.
pagingControlHeight | 更改轮播图小点儿的高度。
currentPage | 正在显示的当前轮播图

### ScrollableView 的方法

Method | Description
--- | ---
scrollToView() | 滚动到哪个图片上.
addView() | 动态的增加View
removeView() | 动态的删除View

