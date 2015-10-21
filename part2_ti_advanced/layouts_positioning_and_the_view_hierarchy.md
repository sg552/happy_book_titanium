TODO: 图片不是自己的

#Layouts, Positioning, and the View Hierarchy

这一章节，我们要学习如何使用Titanium提供的各种位置属性来给你的UI设置布局。以及各种Titanium里的坐标系统，视图层级，位置规则。

我们来看看有哪些因素可以影响你的App里UI的布局元素：

- Units（单位）

- The coordinates grid（坐标网格）

- Positioning and the view hierarchy（位置以及视图层级）

- Layout modes（布局模式）

- zIndex & default stacking order

##Units

UI元素的放置和尺寸都是由一个数值加上一个默认的或者特定单位,如: **10dp**。如果你没有指定特殊的单位，那么认为是使用了系统默认单位,该默认单位在*tiapp.xml*定义,同时也能够修改单位。

首先我们需要先了解两个我们会经常使用到概念的定义

- dip: Density-independent pixels（密度独立像素），是能基于特定平台默认像素和设备的物理像素进行转换适配的一种单位。

- System unit:根据当前系统的情况来设置默认单位，在Android上的System unit是像素，在iOS上是dip。

还支持的单位有：

- 绝对单位

 - px:pixels

 - mm:millimeters

 - cm:centimeters

 - im:inches

 - dp/dip:Density-independent pixels (有时又叫做"points")

    - Android：实际像素 ＝ dip * (screen density)/160

    - iOS：实际像素 ＝ dip * (screen density)/163(实际上普通屏幕上 1dip=1px, retina屏幕上 1dip=2px)

+ 相对单位

 + %:父类尺寸的百分比

    + 对于x轴上的值（width，left，right，center.x），都是相对于父级的宽度来说

    + 对于y轴上的值（height，top，bottom，center.y），都是相对于父级的高度来说

你可以在`controllers`创建一个View，并给它top,left,width分别不同的单位：

```javascript
var view = Ti.UI.createView({
  /* 一般不会像下面这样混合使用，这里只是做一个示例 */
  top: '10mm',
  left: '5px',
  width: '30%',
  height: 50 /* 这里就会使用系统默认的单位 */
});
```

###Setting default units in tiapp.xml(设置默认单位)

你可以在tiapp.xml文件中设置你想要的系统默认值，如下：

```xml
<property name="ti.ui.defaultunit" type="string">value</property>
```
当value是px,mm,cm,in,dp,dip或者系统单位，新的系统单位就是上面的这些平台独立单位。

##The coordinates grid

Titanium使用网格坐标来设置布局。网格位置是基于系统单位（平台独立单位）的。这意味着，在iOS上默认的，元素是被放置在一个密度独立(density-independent)的网格中。在Android上，是被放置在一个密度依赖(density-dependent)的网格中。这样的网格效果就是，在iOS上，我们总会看到元素在相同的位置上，不管这个屏幕的实际像素是多少。在Android上，元素在绝对位置会出现在相同位置，但可能在不同的设备上会有布局上的不同。

- iPhone 不管是普通屏幕还是Retina屏幕，都是基于320x480dip 的网格

- iPad 是基于1024x768dip 的网格

- Android设备屏幕有很多种，可以看看下面不同emulator的例子：
  - HVGA emulator 是320x480 px

  - WVGA800 emulator 是480x800 px

  - WVGA854 emulator 是480x854 px

在Android上，你可以像iOS的density-independent网格布局一样，指定dp或者dip(甚至在tiapp.xml文件里设置app级别的默认值)。

##Positioning and dimensions of elements

Titanium中元素在它们的父级容器中（比如window，view）是绝对位置，根据你设置的位置属性，被引用的那个点会居于父类容器的top，left，bottom或者right角落上。我们称这个为“view hierarchy(视图层级)”。这其中的属性解释如下：

- top 和 left:which specify the grid position of the element's top/left corner relative to the parent's top/left corner.

- bottom 和 right:which specify the grid position of the element's bottom/right corner relative to the parent's bottom/right corner.

- center:which species the position of the element's center point relative to the parent's top/left corner.

(`size` provides the rendered size of the view, and thus is only available once both it and its ancestors have been fully drawn. This means it is also a read-only property; a dictionary with two properties, width and height.)

你可以通过定义`width`和`height`的属性来设置指定的元素的大小。如果没有设置`width`和`height`，但是设置了`top`和`bottom`，对应的元素就会根据父类容器来进行一个绝对的设置。对于只设置`left`和`right`也是一样的。

在下面的例子中，红色的view在window中占据着20x20point的top/left绝对位置，黄色的view占据着100point的bottom/right的绝对位置，蓝色的view的中间是在坐标(160,240)的位置，宽度为50，这就一意味着它的左上角坐标为(110,190)。绿色的view因为它的top为负值，所以它就在屏幕的下方。

如图所示：

![layout](/images/layout.png)

代码如下：
```javascript
var win = Ti.UI.createWindow({
  backgroundColor:'#fff'
});
var redview = Ti.UI.createView({
    top:20,
  left:20,
    width:10,
    height:10,
    backgroundColor:"red"
});
win.add(redview);
var yellowview = Ti.UI.createView({
    bottom:100,
  right:100,
    width:10,
    height:10,
    backgroundColor:"yellow"
});
win.add(yellowview);
var blueview = Ti.UI.createView({
  center: {x: 160, y: 240},
  width:50,
  height:50,
  backgroundColor:"blue"
});
win.add(blueview);
var greenview = Ti.UI.createView({
    top:-20,
    width:10,
    height:10,
    backgroundColor:"green"
});
win.add(greenview);
win.open();
```

##Layout modes

Titanium的window或者view们可以有选择下面三种布局中的一种进行设置：

- aboslute(绝对布局):这是一个默认的布局，你指定一个元素的网格坐标位置，让它居于父类容器的左上角或者右下角的位置。

- vertical(垂直布局):这个布局中，所有子view都是垂直排列。子view的`top`属性就变了，它的指的是离它上面的那个兄弟view的底边的距离。

- horizontal(水平布局):这个布局中，所有子view都是水平放置。子view的`left`属性也变了，它指的是离它左边的那个兄弟view的右边的距离。

```javascript
var win = Ti.UI.createWindow({
  backgroundColor:'#fff'
});
// uses grid-drawing module from https://gist.github.com/1187384
// to draw grid lines every 20 points
var grid = require('gridlines');
grid.drawgrid(20,win);
// draw a view that fills the window and set its layout property
var view = Ti.UI.createView({
  backgroundColor:'transparent',
  top:0,
  left:0,
  width:'100%',
  height:'100%',
  layout:'vertical'
});
// simple function for making colored boxes
function makeView(color) {
  return Ti.UI.createView({
      top:20,
      left:20,
      width:20,
      height:20,
      backgroundColor:color
  });
}
view.add(makeView('red'));
view.add(makeView('yellow'));
view.add(makeView('blue'));
view.add(makeView('green'));
win.add(view);
win.open();
```

效果如图：
![](http://image.happysoft.cc/image/166/vert_and_horiz.png)

##Auto Size Behaviors

Titanium支持元素大小进行自动适配--“auto”。但是在Titanium 2.0的时候，这个属性就被反对使用了。在之前，这个“auto”属性是用于设置高度和宽度的，也应该是“对给定的view和它的内容设置合理的大小”。这种模糊的描述会导致在实现跨平台的时候，效果不一致。

现在被两个明确的行为给代替了：SIZE和FILL。你可以指定`Ti.UI.SIZE`或者`Ti.UI.FILL`来明确地实现“自动适配”的行为。`Ti.UI.SIZE`意思是：根据一个view里面的内容来设置自己的大小值。`Ti.UI.FILL`的意思是：根据父类容器的大小来设置自己的大小值（填充满父类容器）。要注意的是，如果设置了`Ti.UI.FILL`的同时layout属性也不是`aboslute`，会把它后面的其他兄弟view给挤到看不见。

SIZE views | FILL views | Mixed behavior
--- | --- | ---
Button | Window | Toolbar:FILL for width, SIZE for height
Label | View | TableViewRow:FILL for width, SIZE for height
ImageView | TabGroup | Slider:FILL for width, SIZE for height
ProgressBar | TableView |
Switch | WebView |
TextArea | ScrollView |
TextField | ScrollabelView |
Picker | |
SearchBar | |
ButtonBar | |
TableViewSection | |

###ScrollView Content Sizes

对于ScrollView，`contentWidth`和`contentHeight`也可以被设置成“auto”或者“Ti.UI.SIZE”，下面就是这两种情况会产生的行为：
- 当所有的子view都有FILL行为时，scrollview的物理区域都会被充斥满。

- 否则，内容显示区里的内容会按照向下和向右方向扩充。有时候，最底下的view于最右边的view可能就是同一个view。

##zIndex & default stacking

你可以通过`zIndex`来设置一个view在另一个view的上面。默认地，你把一些子view添加到一个父类容器里，后添加进去会覆盖住先添加进去的，按照后来居上的原则。但是你可以给它们设置`zIndex`，数值越大，层级越高。

