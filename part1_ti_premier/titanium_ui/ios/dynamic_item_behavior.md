# Titanium.UI.iOS. DynamicItemBehavior

> 仅支持IOS且版本不小于IOS 7.0的手机或模拟器

为密度和抵抗性的动态行为提供配置,当给item力量去碰撞,根据不同密度产生的行为。

一个简单的碰撞例子(官方文档),两个不同秘密密度的block有不同抵抗力,给它两个相反的力量去碰撞产生的动画效果,`Ti.UI.iOS.createPushBehavior`是推力行为,后文有介绍。如下图所示:

![dynamicItem_behavior](http://image.happysoft.cc/image/61/titanium_ui_ios_ dynamicItem_behavior.gif)

代码示例:

```javascript
var win = Ti.UI.createWindow({backgroundColor: 'white', fullscreen: true});

// Create an Animator object using the window as the coordinate system
var animator = Ti.UI.iOS.createAnimator({referenceView: win});

// Create a red block
var redBlock = Ti.UI.createView({
    backgroundColor: 'red',
    width: 25,
    height: 25,
    top: 25,
    left: 25
});

// Change the physics attributes of the red block
var redDynamic = Ti.UI.iOS.createDynamicItemBehavior({
    density: 20.0,
    angularResistance: 1.0,
    friction: 1.0,
    resistance: 1.0,
    allowsRotation: false
});
redDynamic.addItem(redBlock);

// Apply a left push to the red block
var redPush = Ti.UI.iOS.createPushBehavior({
    pushDirection: {x: 2.0, y: 0.0}
});
redPush.addItem(redBlock);

// Create a blue block
var blueBlock = Ti.UI.createView({
    backgroundColor: 'blue',
    width: 50,
    height: 50,
    top: 25,
    right: 25
});

// Change the physics attributes of the blue block
var blueDynamic = Ti.UI.iOS.createDynamicItemBehavior({
    elasticity: 1.0,
});
blueDynamic.addItem(blueBlock);

// Apply a right push to the blue block
var bluePush = Ti.UI.iOS.createPushBehavior({
    pushDirection: {x: -2.0, y: 0.0}
});
bluePush.addItem(blueBlock);

// Create the collision behavior so the items can collide
var collision = Ti.UI.iOS.createCollisionBehavior();
collision.addItem(redBlock);
collision.addItem(blueBlock);

animator.addBehavior(redDynamic);
animator.addBehavior(redPush);
animator.addBehavior(blueDynamic);
animator.addBehavior(bluePush);
animator.addBehavior(collision);

// Start the animation when the window opens
win.addEventListener('open', function(e){
    animator.startAnimator();
});

win.add(redBlock);
win.add(blueBlock);
win.open();
```