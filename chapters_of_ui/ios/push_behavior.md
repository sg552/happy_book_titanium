# PushBehavior

动画组件, 产生一个推动的行为。

效果如图：

![push behavior](/images/ui_ios_push_behavior.gif)

## 例子

```js
var win = Ti.UI.createWindow({backgroundColor: 'white', fullscreen: true});

var animator = Ti.UI.iOS.createAnimator({referenceView: win});

var block = Ti.UI.createView({
    width: 100,
    height: 100,
    backgroundColor: 'blue',
    transform: Ti.UI.create2DMatrix({ rotate: 45 })
});

// 建立碰撞行为
var collision = Ti.UI.iOS.createCollisionBehavior();
collision.addItem(block);
animator.addBehavior(collision);

// 推动一下
var push = Ti.UI.iOS.createPushBehavior({
    pushDirection: {x: 0.0, y: 1.0},
    pushMode: Ti.UI.iOS.PUSH_MODE_INSTANTANEOUS
});
push.addItem(block);
animator.addBehavior(push);

// 每次只要一停止，就再给它一个随机的力
animator.addEventListener('pause', function(e){
    push.angle = 2 * Math.PI * Math.random();
    push.magnitude = Math.random() * 5 + 5;
    push.active = true;
});

animator.addEventListener('resume', function(e){
    Ti.API.info(JSON.stringify(
        'push force: ' + push.magnitude * 100 + " points/s^2 @ "
        + (push.angle * 360 / (2 * Math.PI)) + " degrees")
    );
});

win.addEventListener('open', function(e){
    animator.startAnimator();
});

win.add(block);
win.open();
```

- 可以通过设置`angle`和`magnitude`属性，或者设置`pushDiretion`属性来定义个矢量力。
- 使用`addItem()`方法来把行为应用到item上。
- 把行为添加到Animator对象上。
