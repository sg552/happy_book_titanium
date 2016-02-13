# 动画

动画也被叫做'eye-candy（眼睛糖果）'，是能吸引用户注意力的法宝。
把Animation运用的得当的话，会让你的app变的更专业。

## 基本动画

最基础的Animation，是要改变UI组件的属性的值。比如它们的`top` ，`left`，
`backgroundColor`，`opacity`。你可以使用`animate()`来给任何继承自
`Ti.UI.View`的组件添加属性变化的动画。该方法接收两个参数：

- Ti.UI.Animation对象: 描述的是这个组件在动画完成时，将会变成的状态。
- 回调函数: 会在动画完成的时候被调用。

下面函数，演示了点击后在两秒内慢慢消失，再过两秒慢慢出现。

![basic](/images/senior_basic_animation.gif)

```js
box.addEventListener('click', function(){
  box.animate({
    opacity:0,
    duration:2000
  }, function(){
    box.animate({
      opacity:1,
      duration:2000
    });
  });
});
```

上面代码等同于下面：

```javascript
var a = Ti.UI.createAnimation({
  opacity:0,
  duration:2000
});
var b = Ti.UI.createAnimation({
  opacity:1,
  duration:2000
});
box.addEventListener('click', function(){
  box.animate(a, function(){
    box.animate(b);
  });
});
```

## Matrix animations (矩阵动画)

Matrix animations 也叫做transformations(变换)。设置x和y坐标就相当于设置元素的边。
矩阵变换通过改变坐标来改变元素。可以做出2d的变化（通过xy坐标），
也可以做出3d的变化（通过xyz坐标）。另外可以缩小，翻转，平移，扭曲任何组件。

### 2D matrix animations

Android平台和iOS平台都支持2D Matix animations(二维动画)。

我们需要实例化一个`Ti.UI.2DMatrix`对象，再给你的目标组件设置参数。
最后再创建一个Animation对象，把`transform`熟悉值设为你创建的2d matrix对象
(`matrix2d`)。

![matrix2d](/images/senior_animation_matrix_2d.gif)

```js
var win = Ti.UI.createWindow({ backgroundColor: 'white', });

var box = Ti.UI.createView({
  backgroundColor: 'blue',
  width: 150,
  height: 150
});

var matrix2d = Ti.UI.create2DMatrix();
// 旋转20度
matrix2d = matrix2d.rotate(20);
// 放大为原来的1.5倍
matrix2d = matrix2d.scale(1.5);
var a = Ti.UI.createAnimation({
  transform: matrix2d,
  duration: 2000,
  autoreverse: true,
  repeat: 3
});
// 启动动画
box.animate(a);

box.addEventListener('click', function(){
  box.animate(a);
})

win.add(box);
win.open();

```

### 3D matrix animations

仅支持iOS.

3D matrix animations是在三维空间的变换，同样的，也可以翻转，缩放等。
但是3d 虚拟对象是没有用的。并且只有iOS才支持3d matrix 。

![3d matrix](/images/senior_animation_matrix_3d.gif)
```js
var win = Ti.UI.createWindow({ backgroundColor: 'white', });

var box = Ti.UI.createView({
  backgroundColor: 'blue',
  width: 150,
  height: 150
});

var matrix3d = Ti.UI.create3DMatrix();
// 下面代码的180度，是专门用于旋转
// 1, 1, 0 则是分别对应 x,y,z 向量
matrix3d = matrix3d.rotate(180, 1, 1, 0);

// 分别在 x,y,z三个维度上放大2倍
matrix3d = matrix3d.scale(2, 2, 2);

var a = Ti.UI.createAnimation({
  transform: matrix3d,
  duration: 2000,
  autoreverse: true,
  repeat: 0
});

box.addEventListener('click', function(){
  box.animate(a);
})

win.add(box);
win.open();
```

### Transitons(变换)

仅限于iOS 7+

Transiton是内置在切换window或者view时使用的animations里。`transition`是
Animation(动画对象)的参数,接着可以定义window或者view的初始状态和最终状态,
最后定义`transition`的类型。

```js
// container 是定义好的view
var selectedIndex = 0;
container.addEventListener('click', function(){
  if (selectedIndex%2 == 0) {
    container.animate({
      view:box2,
      transition:Ti.UI.iPhone.AnimationStyle.FLIP_FROM_LEFT
    });
  }
  else {
    container.animate({
      view:box1,
      transition:Ti.UI.iPhone.AnimationStyle.FLIP_FROM_RIGHT
    });
  }
  selectedIndex++;
});

```
在NavigationWindow或者Tab中的window里使用transition animation，
需要用到window的`transitionAnimation`参数。


