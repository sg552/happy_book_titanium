Welcome to Ti Window World!

如果说，之前提到的View是各种UI元素的container的话，那么Window就是所有View的container。

所以，从这个角度讲，Window是top-level container。

创建一个简单的Window的代码为：
```javascript
var win  = Titanium.UI.createWindow({
title:'Tab 1',
backgroundColor:'#fff'
});
```

使用Alloy框架创建一个Window的代码为
```xml
<Window title="Tab 1" backgroundColor="#fff">
</Window>
```

在Window里面添加一个UI组件，比如说一个Label的例子为:
```javascript
var win = Titanium.UI.createWindow({
title:'Tab 1',
backgroundColor:'#fff'
});
var label = Titanium.UI.createLabel({
color:'#999',
text:'I am Window 1',
font:{fontSize:20,fontFamily:'Helvetica Neue'},
textAlign:'center',
width:'auto'
});
window.add(label);
window.open();
```
使用Alloy框架的代码为：
```xml
<Window title="Tab 1" backgroundColor="#fff">
<Label text="I am a label">
</Label>
</Window>
```
注意：因为Alloy框架中，对font的特殊处理，字体的大小要写在stss文件里面才可以生效。所以这里的XML先省去设置字体的大小设置。

这里需要提及的有window属性中有一些特有的属性

```
LeftNavButton
LeftNavButtons
Title
transitionAnimation
```
以及一些能够包含window的特殊UI如:

```
NavigationWindow
SplitWindow
TabGroup
Tab
NavigationGroup
```
这些属性能够影响Window的导航栏效果,动画效果等等。
之前很多项目都是自定义一些View来取代Window自带的导航栏效果。增加了多样式的情况下却增加了很多代码与适配难度,体验性和动画效果也并不流畅。希望同学们做项目的过程中一定需要多和UI,产品经理沟通并在产品实现效果与付出的代价之间做平衡。
