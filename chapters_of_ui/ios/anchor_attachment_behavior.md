# AnchorAttachmentBehavior

> 要求ios版本7.0+

设置一个锚点，产生钟摆一样的行为。


示例动画:

![钟摆行为](/images/ui_ios_zhong_bai_xing_wei.gif)

下面创建一个AnchorAttachmentBehavior行为,参数是anchor(锚点位置)和item(小圆圈)。

```js
var win = Ti.UI.createWindow({backgroundColor: 'white', fullscreen: true});

// 新建一个animator
var animator = Ti.UI.iOS.createAnimator({referenceView: win});

// 红色圆点
var redCircle = Ti.UI.createView({
    backgroundColor: 'red',
    width: 30,
    height: 30,
    borderRadius: 15,
    top: 10,
    left: 25
});

var WIDTH = Ti.Platform.displayCaps.platformWidth;

// 定义锚点
var anchor = Ti.UI.iOS.createAnchorAttachmentBehavior({
    anchor: {x: WIDTH/2, y: 50},
    item: redCircle
});
animator.addBehavior(anchor);

// 模拟重力
var gravity = Ti.UI.iOS.createGravityBehavior({
    gravityDirection: {x: 0.0, y: 1.0}
});
gravity.addItem(redCircle);
animator.addBehavior(gravity);

win.addEventListener('open', function(e){
  animator.startAnimator();
});

win.add(redCircle);
win.open();
```

- WIDTH: 屏幕宽度,
- anchor: 定义了锚点坐标
- item: 定义了要绑定锚点的对象。
- Ti.UI.iOS.createGravityBehavior(): 创建引力并提供`y`轴方向的向量。
并且将`redCircle`绑定引力实例。
- 最后给动画添加行为(引力和锚点)
- startAnimator: 开始动画。
