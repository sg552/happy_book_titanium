# View

View是Titanium最基本的组件，可以认为成是白色的画布，
我们可以在这上面勾勒出我们想要的各种图形。

```js
var view = Titanium.UI.createView({
  borderRadius:10,
  backgroundColor:'red',
  width:50,
  height:50
});
window.add(view);
```

View的样式可以被大部分的UI组件所使用，因为大部分的UI都是View的子类。 具体的样式
请看 [View的各种样式](styles.md)
