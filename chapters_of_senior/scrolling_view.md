TODO：图片不是自己的，属性介绍类同

#Scrolling View

Titanium提供两种可以滑动的view，`ScrollView`和`ScrollableView`。虽然名字很像很接近，但是功能上确是有很多的不同。

可以先看看下面两张图片大概区别下：
![](http://image.happysoft.cc/image/168/Screen_shot_2011-12-08_at_11.42.09_AM.png)

从上面可以看出：

+ ScrollView是一个可滑动的内容容器，它不需要全部充满整个视图窗口。用户可以用手指任意方向的拖动来实现滑动。

+ ScrollableView是一个可以容纳多个子view的全屏控件。类似于coverflow view 或者类似于水平滑动来切换图片的相册。通常，ScrollabelView都会带一个page indicator（滚动条）。ScrollabelView只能水平的滑动！

##ScrollView

你可以用`Ti.UI.createScrollView()`方法来创建ScrollView，如下：

```javascript
var sv = Ti.UI.createScrollView({
  height: 200,
  width: 200,
  /* left & right work too */
  contentHeight: Ti.UI.SIZE,
  contentWidth: Ti.UI.SIZE
})
```

`height`和`width`定义了ScrollView在window中要占据多大的空间 。`contentHeight`和`contentWidth`定义了内容区域在ScrollView中占据的区域大小。默认的，这个是用来设置内容的大小的。如果你设置的contentWidth和contentHeight小于内容所需要的大小的话，会造成内容区域被挤压了。如果你设定的又太大了，那么又会显示多出来的空间。

###ScrollView的属性

Property | Description
--- | ---
zoomScale, minZoomScale, maxZoomScale (缩放) | You can control zooming of the content within the ScrollView with these properties. Each accepts a numeric value between 0 and 1.
horizontalBounce, verticalBounce (反弹效果) | (iOS only) These Boolean values control whether the ScrollView displays that "bounce" effect when the user has reached the end of the scrolling content.
showHorizontalScrollIndicator, showVerticalScrollIndicator (滚动条) | These Boolean values control whether the scroll indicator (scrollbar-like gizmo) is displayed.
scrollType (滚动类型) | On Android, you can set the ScrollView to either "vertical" or "horizontal" but not both.
canCancelEvents | On iOS, you can set this value to true (default) so that events are handled by the ScrollView rather than the views it contains.

####Android上的要注意的问题

在Android上，可以水平滑动也可以垂直滑动，但不会同时支持两个方向。如果你没有设定指定的scrollType的话，具体能怎么滑动就的依据下面这两条逻辑来看了：

+ 如果你设置了width和contentWidth的时候，这相当于把ScrollType设置为`vertical`

+ 如果你设置了height和contentHeight的时候，这相当于把ScrollType设置为`horizontal`

####ScrollView events

给ScrollView 添加监听事件就像给Button，Label等一样简单。

##ScrollabelView

scrollableView是用来显示一群`Ti.UI.VIEW`的对象的可滑动容器。你可以先于scrollableView之前创建它的子view，也可以在之后创建。如下：

```javascript
var view1 = Titanium.UI.createView({backgroundColor:'#123'});
var view2 = Titanium.UI.createView({backgroundColor:'#234'});
var view3 = Titanium.UI.createView({backgroundColor:'#345'});
var scrollable = Titanium.UI.createScrollableView({
	views:[view1,view2,view3],
  	showPagingControl: true
});
win.add(scrollable);
// add another view
var view4 = Titanium.UI.createView({backgroundColor:'#456'});
scrollable.addView(view4);
// and you could remove a view with
scrollable.removeView(view1);
```
通常你应该先创建view们，然后再把它们以数组的形式添加到ScrollableView中。理论上，这个方法会让视图渲染最快的。

###ScrollableView properties

Property | Description
--- | ---
showPagingControl | Boolean, set to false (default) to hide the paging control (the dots that show which page you're viewing)
pagingControlColor | Set the background color for the paging control; you can't control the color of the dots.
pagingControlHeight | Set the height of the paging control area.
currentPage | This property accepts an index number of the view to display (zero-based, so currentPage=2 would show the third view within the ScrollableView)
cacheSize | This iOS-only property accepts an integer value to control the number of views pre-rendered. See the API docs for considerations when using this property.

###ScrollableView methods

Method | Description
--- | ---
scrollToView() | Accepts an integer or object reference of the sub-view to scroll into view within the ScrollableView.
addView() | Adds a view to the ScrollableView, as shown in the code above.
removeView() | Removes a view from the ScrollableView, as shown in the code above.


###ScrollableView events

同上，ScrollableView也支持最标准的事件处理。
