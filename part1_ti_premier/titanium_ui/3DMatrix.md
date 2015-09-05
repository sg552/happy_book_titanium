#3DMatrix
3D Matrix对象是用于盛放一个三维仿射变换矩阵的数值。一般用于实现一个三维空间对象的旋转，缩放，平移或者倾斜。
##实例对象
使用`Titanium.UI.create3DMatrix`方法来实例化对象
区别于2DMatrix的是：这是三维矩阵，所以它的方法里的参数就会比二维的要多一个，比如`translate()`方法的参数就比二维的`translate()`方法多一个。毕竟多一维。
下面来实现一个效果，让一个label从距离屏幕顶部100px的地方向下移动200px。
```javascript
var win = Ti.UI.createWindow({
  backgroundColor: 'white'
});

var label = Ti.UI.createLabel({
  font:{fontSize:50},
  text:'Titanium',
  textAlign:'center',
  top: 100
});
win.add(label);

var button = Ti.UI.createButton({
  title:'Animate',
  bottom:20,
  width:200, height:40
});
win.add(button);

button.addEventListener('click', function(){
  var t1 = Ti.UI.create3DMatrix();
  t1 = t1.translate(0, 100, 200);
  t1.m34 = 1.0/-90;
  var a1 = Ti.UI.createAnimation();
  a1.transform = t1;
  a1.duration = 800;
  label.animate(a1);
});
win.open();
```
