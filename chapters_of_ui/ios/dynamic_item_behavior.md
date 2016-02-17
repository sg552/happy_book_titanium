# DynamicItemBehavior

> 仅支持iOS7.0+

为密度和抗撞击性(resistance)的动态行为配置,当给item力量去碰撞,
根据不同密度产生的行为。

两个不同密度的小方框有不同抗撞击力,
给它两个相反的力量去碰撞产生的动画效果,
如下图所示:

![dynamicItem_behavior](/images/ui_ios_dynamic_item_behavior.gif)

代码示例:

```js
var win = Ti.UI.createWindow({backgroundColor: 'white', fullscreen: true});

var animator = Ti.UI.iOS.createAnimator({referenceView: win});

var redBlock = Ti.UI.createView({
    backgroundColor: 'red',
    width: 25,
    height: 25,
    top: 25,
    left: 25
});

var redDynamic = Ti.UI.iOS.createDynamicItemBehavior({
    density: 20.0,
    angularResistance: 1.0,
    friction: 1.0,
    resistance: 1.0,
    allowsRotation: false
});
redDynamic.addItem(redBlock);

// 从左方推动红色小方框
var redPush = Ti.UI.iOS.createPushBehavior({
    pushDirection: {x: 2.0, y: 0.0}
});
redPush.addItem(redBlock);

var blueBlock = Ti.UI.createView({
    backgroundColor: 'blue',
    width: 50,
    height: 50,
    top: 25,
    right: 25
});

// 给蓝色小方框的弹性设置成1.0
var blueDynamic = Ti.UI.iOS.createDynamicItemBehavior({
    elasticity: 1.0,
});
blueDynamic.addItem(blueBlock);

// 从右方推动蓝色小方框
var bluePush = Ti.UI.iOS.createPushBehavior({
    pushDirection: {x: -2.0, y: 0.0}
});
bluePush.addItem(blueBlock);

// 碰撞开始
var collision = Ti.UI.iOS.createCollisionBehavior();
collision.addItem(redBlock);
collision.addItem(blueBlock);

animator.addBehavior(redDynamic);
animator.addBehavior(redPush);
animator.addBehavior(blueDynamic);
animator.addBehavior(bluePush);
animator.addBehavior(collision);

// 开始动画
win.addEventListener('open', function(e){
    animator.startAnimator();
});

win.add(redBlock);
win.add(blueBlock);
win.open();
```
