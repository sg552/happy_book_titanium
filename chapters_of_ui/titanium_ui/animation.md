#Animation

一个Animation对象是作用于一个view上的。一个Animation对象它实际就是在描述一个动画的各种参数，比如最基本的它可以描述单次动画的开始状态和结束状态以及这段动画持续的时间。
当animate被作用在一个view上，这个view会从最开始的状态变化到由animation对象所定义的各种参数的最终状态。这些定义的参数中可以包括：position,size,transformation matrix和透明度。
Animation可以在结束之前实现与自己相反的效果，并且根据你设定的次数进行重复。如果要实现更复杂的效果，可以融合多个animation在一起，按顺序的执行。

##使用方法
使用`Titanium.UI.createAnimation`方法来实例一个animation对象。

##注意
当你在给一个view来创建动画的时候，如果你设定这个view的size或者position，这个view的实际各种布局参数是不会被这个动画所改变的。

###iOS
iOS支持2D Matrix和3D Matrix。在iOS上，你可以定义一个动画曲线或者一个舒缓作用的去控制动画效果的每一步。比如我们可以在给animation的`curve`属性设置成`ANIMATION_CURVE_EASE_IN`，这样就会实现一个开始效果速度慢最后速度加快的动画。
iOS同样支持animation作用在window和view上，你也可以通过设置`Titanium.UI.iPhone.AnimationStyle`来实现你想要的`transition`效果风格。

###Android
Android只支持2D Matrix。需要注意的是`2DMatrix.ratate`这个方法是有些特殊的。当它的参数只有一个的时候，意味着是从0度翻转带参数的那个角度；如果是两个参数，则是从第一个参数所代表的角度翻转到第二个参数所代表的角度。Android不支持像iOS一样的动画曲线或者舒缓功能，动画效果永远是从开始效果线性的执行到最终效果。

##使用例子

###简单的把view做成动画
让view的背景颜色在规定的时间内进行变化

```javascript
var view = Titanium.UI.createView({
  backgroundColor:'red'
});
var animation = Titanium.UI.createAnimation();
animation.backgroundColor = 'black';
animation.duration = 1000;
var animationHandler = function() {
  animation.removeEventListener('complete',animationHandler);
  animation.backgroundColor = 'orange';
  view.animate(animation);
};
animation.addEventListener('complete',animationHandler);
view.animate(animation);
```

效果如图所示：
![简单的动画效果](http://image.happysoft.cc/image/46/hua1.gif)

###简单的矩阵变幻效果
点击红色方块，方块旋转，并放大，且重复三次。

```javascript
var box = Ti.UI.createView({
  backgroundColor : 'red',
  height : '100',
  width : '100'
});
win.add(box);

box.addEventListener('click', function() {
    var matrix = Ti.UI.create2DMatrix()
    matrix = matrix.rotate(180);
    matrix = matrix.scale(2, 2);
    var a = Ti.UI.createAnimation({
      transform : matrix,
      duration : 2000,
      autoreverse : true,
      repeat : 3
    });
    box.animate(a);
});
```
效果如图：
![简单矩阵效果](http://image.happysoft.cc/image/47/hua2.gif)

###锚点效果
在iOS和Android下

```javascript
var animationType = [
  { name: 'Top Left', anchorPoint: {x:0, y:0} },
  { name: 'Top Right', anchorPoint: {x:1, y:0} },
  { name: 'Bottom Left', anchorPoint: {x:0, y:1} },
  { name: 'Bottom Right', anchorPoint: {x:1, y:1} },
  { name: 'Center', anchorPoint: {x:0.5, y:0.5} }
];
var animationTypeLength = animationType.length;
var animationCount = 0;
var animationTypePointer = 0;

var t = Ti.UI.create2DMatrix();
t = t.rotate(90);

// animation properties
var a = {
  transform: t,
  duration: 2000,
  autoreverse: true
};

Ti.UI.backgroundColor = 'white';
var win = Ti.UI.createWindow();

var view = Ti.UI.createView({
  backgroundColor:'#336699',
  width:100, height:100
});
win.add(view);

var button = Ti.UI.createButton({
  title:'Animate ' + animationType[animationTypePointer].name,
  height: (Ti.UI.Android) ? 80 : 40,
  width: (Ti.UI.Android) ? 300 : 200,
  top:30
});
win.add(button);

function updateButton(name){
  button.title = 'Animate ' + name;
}

button.addEventListener('click', function(){
    // set new anchorPoint on animation for Android
    a.anchorPoint = animationType[animationTypePointer].anchorPoint;

    // set new anchorPoint on view for iOS
    view.anchorPoint = animationType[animationTypePointer].anchorPoint;

    animationCount++;

    // determine position of next object in animationType array or return to first item
    // using modulus operator
    animationTypePointer = animationCount % animationTypeLength;

    // animate view, followed by callback to set next button title
    view.animate(a, function(){
      updateButton(animationType[animationTypePointer].name);
      });
    });

win.open();
```

效果如图所示：
![锚点](http://image.happysoft.cc/image/49/hua3.gif)
