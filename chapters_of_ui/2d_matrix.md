#2D Matrix

用于实现一个二维空间对象的旋转，缩放，平移或者倾斜。

## 实例对象

使用 `Titanium.UI.create2DMatrix` 方法来实例化对象, 如：

```js
var m = Ti.UI.create2DMatrix({
  //旋转45度
  rotate: 45
});
```

下面来看看一个具体例子：让一个圆形view在Y轴方向移动：

```javascript
// 创建一个window
var win = Ti.UI.createWindow({
  backgroundColor: 'white'
});

// 创建一个圆圈
var circle = Ti.UI.createView({
  width: 50,
  height: 50,
  borderRadius: 25,
  backgroundColor: 'red',
  top: 100
});

win.add(circle);

// 创建一个触发动画的按钮
var button = Ti.UI.createButton({
  title:'Animate',
  bottom:20,
  width:200,
  height:40
});

win.add(button);

// 绑定点击事件
button.addEventListener('click', function(){
  var t = Ti.UI.create2DMatrix();
  t = t.translate(0, 300); // 传递参数给这个对象的translate方法
  var animation = Ti.UI.createAnimation();
  animation.transform = t;
  animation.duration = 800; // 设定动画的时间
  circle.animate(animation); // 执行动画
  });
win.open();
```
