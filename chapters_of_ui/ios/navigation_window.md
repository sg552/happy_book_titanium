# NavigationWindow

用于导航。

所有的NavigationWindow对象都至少要有一个根window，并且不能删除它。
当创建完一个NavigationWindow对象的时候，
要通过`window`属性来设置它的根window。

# 用法

![navigation window](/images/ui_ios_navigation_window.gif)

```js
var red_window = Titanium.UI.createWindow({
  backgroundColor: 'red',
  title: '红色window'
});

var navigation_window = Titanium.UI.iOS.createNavigationWindow({
  window: red_window
});

var blue_window = Titanium.UI.createWindow({
  backgroundColor: 'blue',
  title: '蓝色window'
});

var open_button = Titanium.UI.createButton({
  title: '打开蓝色window'
});

open_button.addEventListener('click', function(){
  // 只要是在导航window中进行的打开，导航window就能记住它。
  navigation_window.openWindow(blue_window, {animated:true});
});

red_window.add(open_button);
var close_button = Titanium.UI.createButton({
  title: '关闭蓝色window'
});
close_button.addEventListener('click', function(){
  navigation_window.closeWindow(blue_window, {animated:false});
});

blue_window.add(close_button);
navigation_window.open();
```

