# Window

Window 包含了多个View. 可以说是View的container。

```javascript
var win  = Titanium.UI.createWindow({
  title:'Tab 1',
  backgroundColor:'#fff'
});
```

在Window里面添加一个Label:

```javascript
var win = Titanium.UI.createWindow({
  title:'Tab 1',
  backgroundColor:'#fff'
});
var label = Titanium.UI.createLabel({
  color:'#999',
  text:'I am Window 1',
  font:{
    fontSize:20,
    fontFamily:'Helvetica Neue'
  },
  textAlign:'center',
  width:'auto'
});
window.add(label);
window.open();
```

Window有很多特有属性, 包括：

- leftNavButton
- leftNavButtons
- title
- transitionAnimation

很多很多。希望大家可以多看官方文档，尽快熟悉。

下面这些UI组件可以包含Window, 自动控制Window的开和关:

- NavigationWindow
- SplitWindow
- TabGroup
- Tab
- NavigationGroup

这些属性能够影响Window的导航栏效果,动画效果等等。

之前很多项目都是自定义一些View来取代Window自带的导航栏效果。
增加了多样式的情况下却增加了很多代码与适配难度,体验性和动画效果也并不流畅。

大家做项目的过程中要多和UI、产品经理沟通, 在产品实现效果与付出的代价之间做平衡。
