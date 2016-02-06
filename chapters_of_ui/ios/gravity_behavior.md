#GravityBehavior
给item加上重力感应的效果。

使用步骤：
+ 使用`Titanium.UI.iOS.createGravityBehavior`方法来创建和定义这样的重力行为。

+ 要定义一个重力矢量(gravity vector)的话，既可以给`angle`和`magnitude`属性设置值，也可以给`gravity
Direction`属性来设置值。

+ 使用`addItem()`方法来把行为应用到item上。

+ 再把行为添加到animator对象上。

```javascript
var win = Ti.UI.createWindow({backgroundColor: 'white', fullscreen: true});

// Create an Animator object using the window as the coordinate system
var animator = Ti.UI.iOS.createAnimator({referenceView: win});

// Create a default collision behavior, using the window edges as boundaries
var collision = Ti.UI.iOS.createCollisionBehavior();

// Simulate Earth's gravity
var gravity = Ti.UI.iOS.createGravityBehavior({
    gravityDirection: {x: 0.0, y: 1.0}
});

var WIDTH = Ti.Platform.displayCaps.platformWidth;
var HEIGHT = Ti.Platform.displayCaps.platformHeight;

// Create a bunch of random blocks; add to the window and behaviors
var blocks = [];
for (var i = 0; i < 20; i++) {
    var r = Math.round(Math.random() * 255);
    var g = Math.round(Math.random() * 255);
    var b = Math.round(Math.random() * 255);
    var rgb = 'rgb(' + r +"," + g + "," + b + ")";

    blocks[i] = Ti.UI.createView({
        width: 25,
        height: 25,
        top: Math.round(Math.random() * (HEIGHT - 25) + 25),
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

// Change the gravity vector when the button is clicked
var button = Ti.UI.createButton({title: 'Change'});
button.addEventListener('click', function(e){
    gravity.gravityDirection = {
        x: (1 - Math.random() * 2),
        y: (1 - Math.random() * 2)
    };
    Ti.API.info('gravity vector: ' + JSON.stringify(gravity.gravityDirection));
});
win.add(button);
win.open();
```
效果如图:

![](http://image.happysoft.cc/image/176/gravity.gif)
