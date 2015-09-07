# Titanium.UI.iOS.CollisionBehavior

> 仅支持IOS且版本不小于IOS 7.0的手机或模拟器

item自身或与边界的碰撞行为。

定义一个边界碰撞行为:

* 定义一个碰撞行为`Titanium.UI.iOS.createCollisionBehavior `
* 绑定item(user `addItem` method)
* 添加碰撞边界,默认为reference view(参考视图)
* 定义一个Animotor object并添加behavior(行为)

下面是一个边界碰撞的例子(官方文档例子):

定义了很多block并添加到`collision `引力和`gravity `边界行为中。最后`animator`(物理动画)添加`Behavior`(行为)并启动`startAnimator()`

效果如下图所示:

![collision_behavior](http://image.happysoft.cc/image/59/titanium_ui_ios_ collision_behavior.gif)

代码如下:

```javascript
var win = Ti.UI.createWindow({backgroundColor: 'white', fullscreen: true});

// Create an Animator object using the window as the coordinate system
var animator = Ti.UI.iOS.createAnimator({referenceView: win});

// Create a default collision behavior, using the window edges as boundaries
var collision = Ti.UI.iOS.createCollisionBehavior();

// Listen for collisions
function report(e) {
    Ti.API.info(JSON.stringify(e.type));
};
collision.addEventListener('itemcollision', report);
collision.addEventListener('boundarycollision', report);

// Simulate Earth's gravity
var gravity = Ti.UI.iOS.createGravityBehavior({
    gravityDirection: {x: 0.0, y: 1.0}
});

var WIDTH = Ti.Platform.displayCaps.platformWidth;
var HEIGHT = Ti.Platform.displayCaps.platformHeight;

// Create a bunch of random blocks; add to the window and behaviors
var blocks = [];   
for (var i = 0; i < 25; i++) {
    var r = Math.round(Math.random() * 255);
    var g = Math.round(Math.random() * 255);
    var b = Math.round(Math.random() * 255);
    var rgb = 'rgb(' + r +"," + g + "," + b + ")";

    blocks[i] = Ti.UI.createView({
        width: 25,
        height: 25,
        top: Math.round(Math.random() * (HEIGHT / 4) + 25),
        left: Math.round(Math.random() * (WIDTH - 25) + 25),
        backgroundColor: rgb
    });
    win.add(blocks[i]);
    collision.addItem(blocks[i]);
    gravity.addItem(blocks[i]);
}

animator.addBehavior(collision);
animator.addBehavior(gravity);

// Start the animation when the window opens
win.addEventListener('open', function(e){
    animator.startAnimator();
});

win.open();
```