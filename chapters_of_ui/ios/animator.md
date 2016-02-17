# Animator

用来产生动画。本节只是大概做个介绍，如果您有意在动画方面发展的话，请深入阅读
Titanium官方文档。（[这个项目也不错](https://github.com/animecyc/TitaniumAnimator) )

Animator要与以下效果一起配合使用：

- AnchorAttachmentBehavior(动画:钟摆行为)
- CollisionBehavior(动画:碰撞行为)
- GravityBehavior(动画:重力行为)
- DynamicItemBehavior(动画:动态物体行为)
- PushBehavior(动画:推力行为)

> iOS版本7.0+

behaviors(行为)定义运动轨迹或规则,item是产生动画的对象。

下面是创建动画的文字说明， 完整例子见
[iOS 钟摆行为](anchor_attachment_behavior.md)。

1.创建animator:

```js
var animator = Titanium.UI.iOS.createAnimator()
```

2.用`referenceView`属性对参考视图对进行关联,任何需要animated的item都需要
是`referenceView`的`child`,且实用碰撞行为是,
item的边缘不能超过`referenceView `的边缘,关联参考视图如下:

```javascript
var animator = Ti.UI.iOS.createAnimator({referenceView: win});
```

3.创建一个或多个behaviors(行为)绑定item

Titanium.UI.iOS.AnchorAttachmentBehavior
Titanium.UI.iOS.CollisionBehavior
Titanium.UI.iOS.DynamicItemBehavior
Titanium.UI.iOS.GravityBehavior
Titanium.UI.iOS.PushBehavior
Titanium.UI.iOS.SnapBehavior
Titanium.UI.iOS.ViewAttachmentBehavior

4.通过`addBehavior method`为`animator`添加行为
5.使用`startAnimator method`启动animator


下面的WIDTH和HEIGHT为`referenceView `的width和height

点位置:

- Top-left corner: (0,0)
- Top-right corner: (WIDTH, 0)
- Center: (WIDTH/2, HEIGHT/2)
- Bottom-left corner: (0, HEIGHT)
- Bottom-right corner: (WIDTH, HEIGHT)

矢量:

- Left: (-x,0)
- Right: (+x,0)
- Up: (0,-y)
- Down: (0,+y)

角度:

- Right: 0 or 2 * pi
- Down: pi / 2
- Left: pi
- Up: pi / 2 * 3

