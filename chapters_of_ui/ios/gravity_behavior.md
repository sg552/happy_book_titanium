# GravityBehavior

动画效果：产生重力感应。

如图:

![gravity](/images/ui_ios_gravity_behavior.gif)

```js
var win = Ti.UI.createWindow({backgroundColor: 'white', fullscreen: true});

var animator = Ti.UI.iOS.createAnimator({referenceView: win});

// 新建默认的碰撞行为
var collision = Ti.UI.iOS.createCollisionBehavior();

// 模拟重力行为
var gravity = Ti.UI.iOS.createGravityBehavior({
    gravityDirection: {x: 0.0, y: 1.0}
});

var WIDTH = Ti.Platform.displayCaps.platformWidth;
var HEIGHT = Ti.Platform.displayCaps.platformHeight;

// 创建一堆小方框
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

// 启动动画
win.addEventListener('open', function(e){
    animator.startAnimator();
});

// 修改重力方向
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

- 要定义一个重力矢量(gravity vector)的话，既可以给`angle`和`magnitude`属性设置值，也可以给`gravity
Direction`属性来设置值。
- 使用`addItem()`方法来把行为应用到item上。
- 再把行为添加到animator对象上。
