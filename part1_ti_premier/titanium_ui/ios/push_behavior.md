#PushBehavior
##实现步骤
+ 用`Titanium.UI.iOS.createPushBehavior`方法创建和定义对应的行为。

+ 可以通过设置`angle`和`magnitude`属性，或者设置`pushDiretion`属性来定义个矢量力。

+ 使用`addItem()`方法来把行为应用到item上。

+ 把行为添加到Animator对象上。

##使用例子
```javascript
var win = Ti.UI.createWindow({backgroundColor: 'white', fullscreen: true});

// Create an Animator object using the window as the coordinate system
var animator = Ti.UI.iOS.createAnimator({referenceView: win});

var block = Ti.UI.createView({
    width: 100,
    height: 100,
    backgroundColor: 'blue',
    transform: Ti.UI.create2DMatrix({ rotate: 45 })
});

// Create a default collision behavior, using the window edges as boundaries
var collision = Ti.UI.iOS.createCollisionBehavior();
collision.addItem(block);
animator.addBehavior(collision);

// Push the block down when the application first starts
var push = Ti.UI.iOS.createPushBehavior({
    pushDirection: {x: 0.0, y: 1.0},
    pushMode: Ti.UI.iOS.PUSH_MODE_INSTANTANEOUS
});
push.addItem(block);
animator.addBehavior(push);

// Apply a new push behavior when the item stops
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

// Start the animation when the window opens
win.addEventListener('open', function(e){
    animator.startAnimator();
});

win.add(block);
win.open();
```

效果如图：
![](http://image.happysoft.cc/image/184/pushforce.gif)
