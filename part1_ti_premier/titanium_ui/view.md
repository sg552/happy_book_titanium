Welcome to Ti UI world!

View是Titanium最基本的组件，可以认为成是白色的画布，我们可以在这上面勾勒出我们想要的各种图形。
简单的创建一个View的代码为:
```javascript
var view = Titanium.UI.createView({
borderRadius:10,
backgroundColor:'red',
width:50,
height:50

});
window.add(view);
```

如果使用Alloy框架的话，代码为：
```xml
<Alloy>
<View id="view" borderRadius="10" backgroundColor="red" width="50" height="50" />
</Alloy>
```

View的更多用法，敬请期待。
