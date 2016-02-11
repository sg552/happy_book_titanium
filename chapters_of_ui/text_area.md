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

## 定制ToolBar

在iOS 上，可以为输入键盘定制ToolBar. 例如下图，注意键盘上方的cancel 和 摄像机图标：

![textarea toolbar](/images/ui_textarea_toolbar.png)

```js
var win = Ti.UI.createWindow({backgroundColor: 'white'});

var camera  = Ti.UI.createButton({
  systemButton: Ti.UI.iPhone.SystemButton.CAMERA
});

var cancel = Ti.UI.createButton({
  systemButton: Ti.UI.iPhone.SystemButton.CANCEL
});

var textarea = Ti.UI.createTextArea({
  color: 'red',
  borderWidth: 2,
  borderColor: 'blue',
  value: 'lalala',
  top: 30,
  width: 400,
  height: 200,
  keyboardToolbar: [cancel, camera],
  keyboardToolbarColor: '#999',
  keyboardToolbarHeight: 40
});

win.add(textarea);
win.open();
```
