TODO: 缺少图片

#Animation

Animation被叫做'eye-candy（眼睛糖果）'，是能吸引用户注意力的法宝。把Animation运用的得当的话，会让你的app变的更专业。

##Basic animations

最基础的Animation，是要改变UI组件的属性的值。比如它们的`top` ，`left`，`backgroundColor`，`opacity`。你可以使用`animate()`方法来给任何继承自`Ti.UI.View`的组件添加属性变化的动画。这个方法接收两个参数：一个Ti.UI.Animation对象和一个回调方法。这个animation对象描述的是这个组件在动画完成时，将会变成的状态。这个回调方法会在动画完成的时候被调用。

```javascript
// box is a Ti.UI.View, when clicked, it fades out of view in 2 seconds, then fades back into view
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

当然，你也可以用下面的代码来实现同样的效果。
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

##Matrix animations

Matrix animations 也叫做transformations。设置x和y坐标就相当于设置元素的边。一个矩阵变换是用数学上的改变坐标来改变元素。你可以做出2d的变化（通过xy坐标），也可以做出3d的变化（通过xyz坐标）。另外，你可以缩小，翻转，平移，扭曲任何组件。

###2D matrix animations

Titanium中Android平台和iOS平台都支持2D Matix animations(二维动画)。

我们需要实例化一个`Ti.UI.2DMatrix`对象，再给你的目标组件设置参数。最后再创建一个Animation对象，把`transform`熟悉值设为你创建的2d matrix对象(`matrix2d`)。

```javascript
var matrix2d = Ti.UI.create2DMatrix();
matrix2d = matrix2d.rotate(20); // in degrees
matrix2d = matrix2d.scale(1.5); // scale to 1.5 times original size
var a = Ti.UI.createAnimation({
  transform: matrix2d,
  duration: 2000,
  autoreverse: true,
  repeat: 3
});
box.animate(a); // set the animation in motion

```
> 当你设置的顺序不一样的时候，可能出现的效果是不一样的。

###3D matrix animations(iOS only)

3D matrix animations是在三维空间的变换，同样的，你也可以翻转，缩放等。但是3d 虚拟对象是没有用的。并且只有iOS才支持3d matrix 。

```javascript
var matrix3d = Ti.UI.create3DMatrix();
// In next statement, the first arg is in degrees and the next three define an xyz vector describing the transformation
matrix3d = matrix3d.rotate(180, 1, 1, 0);
matrix3d = matrix3d.scale(2, 2, 2); // scale factor in the xyz axes
var a = Ti.UI.createAnimation({
  transform: matrix3d,
  duration: 2000,
  autoreverse: true,
  repeat: 3
});
box.animate(a); // set the animation in motion
```

####Transitons

`Transitons`是iOS的专有属性，Transiton是内置在切换window或者view时使用的animations里。`transition`是Animation(动画对象)的参数,接着可以定义window或者view的初始状态和最终状态,最后定义`transition`的类型。

```javascript
// container is a View to which box1 and box2 are added
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
在NavigationWindow或者Tab中的window里使用transition animation，需要用到window的`transitionAnimation`参数。

只支持iOS 7以及之后的版本,用` Titanium.UI.iOS.createTransitionAnimation()`方法创建动画,并让window在打开和关闭的同时有动画效果。

