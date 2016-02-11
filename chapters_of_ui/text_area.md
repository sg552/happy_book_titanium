# Titanium.UI.TextArea

多行文本

![android](/images/ui_textarea_android.png) | ![ios](/images/ui_textarea_ios.png) | ![wp](/images/ui_textarea_wp.png)
:---:|:---:|:---:
Android | iOS | Windows Phone

![text area](/images/ui_textarea.gif)

代码如下：

```js
var win = Ti.UI.createWindow({backgroundColor: 'white'});

var textarea = Ti.UI.createTextArea({
  color: 'red',
  borderWidth: 2,
  borderColor: 'blue',
  value: 'lalala',
  top: 30,
  width: 400,
  height: 200
});

win.add(textarea);
win.open();
```
