# Titanium.UI.iOS.AnchorAttachmentBehavior

> 仅支持IOS且版本不小于IOS 7.0的手机或模拟器

两个锚点之间的动态行为。

```javascript
var WIDTH = Ti.Platform.displayCaps.platformWidth;

// Anchor the red circle to a point near the top-center
var anchor = Ti.UI.iOS.createAnchorAttachmentBehavior({
    anchor: {x: WIDTH/2, y: 50},
    item: redCircle
});
```

`WIDTH`为屏幕高度,`anchor`熟悉定义了锚点坐标,`item`定义了要绑定锚点的对象。

创建一个AnchorAttachmentBehavior行为,参数是anchor(锚点位置)和item(小圆圈)。

示例动画:

![AnchorAttachmentBehavior](http://image.tidev.in/image/58/titanium_ui_ios_ AnchorAttachmentBehavior.gif)

代码示例:

```javascript
var win = Ti.UI.createWindow({backgroundColor: 'white', fullscreen: true});

// Create an Animator object using the window as the coordinate system
var animator = Ti.UI.iOS.createAnimator({referenceView: win});

// Create a red circle to animate
var redCircle = Ti.UI.createView({
    backgroundColor: 'red',
    width: 30,
    height: 30,
    borderRadius: 15,
    top: 10,
    left: 25
});

var WIDTH = Ti.Platform.displayCaps.platformWidth;

// Anchor the red circle to a point near the top-center
var anchor = Ti.UI.iOS.createAnchorAttachmentBehavior({
    anchor: {x: WIDTH/2, y: 50},
    item: redCircle
});
animator.addBehavior(anchor);

// Simulate Earth's gravity to allow the pendulum to swing
var gravity = Ti.UI.iOS.createGravityBehavior({
    gravityDirection: {x: 0.0, y: 1.0}
});
gravity.addItem(redCircle);
animator.addBehavior(gravity);

// Start the animation when the window opens
win.addEventListener('open', function(e){
    animator.startAnimator();
});

win.add(redCircle);
win.open();
```

* `Titanium.UI.iOS.Animator`一个与物理关联的动画,后面的章节会提到。
* `Ti.UI.iOS.createGravityBehavior`是创建引力并提供`y`轴方向的向量。并将`redCircle`绑定引力实例。最后给动画添加行为(引力和锚点)和`tartAnimator`动画。
