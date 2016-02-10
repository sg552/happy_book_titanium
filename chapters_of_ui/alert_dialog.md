#AlertDialog

Titanium提供的alert dialog(对话框)包括:

- 标题（可选）
- 正文
- 按钮

展示时是显示在屏幕的中央。

![android](/images/ui_alertdialog_android.png) | ![ios](/images/ui_alertdialog_ios.png) | ![windows phone](/images/ui_alertdialog_wp.png)
:---:|:---:|:---:
安卓|ios|Windows Phone

## 注意

### Android

在安卓上，默认的alert dialog显示文本信息是由一个标题一个消息文本组成的，
没有任何按钮。用户可以通过手机的物理返回键来关闭它，按钮只是一个可选项。

只有当`buttonNames`这个参数定义赋值，对话框上的按钮才会显示，
并且一般是显示在消息文本的下方。

### iOS

在iOS上，默认的alert dialog显示文本信息是由一个标题一个消息文本，
以及一个单独的按钮来实现的，用户可以通过点击按钮来关闭这个对话框。

按钮也是通过定义赋值给属性`buttonNames`来实现的，并且显示在文本信息的垂直下方。

在iOS 4.0以及之后的版本上，alert dialog在程序被暂停或被挂起的时候会自动地被
取消。这个行为可以避免alert dialog上的属性被持续的设置为`true`。

在iOS 5.0以及之后的版本上，alert dialog可以在设置`style`这个属性值来实现，
对话框可以让用户输入简单的文本，或者做登录和密码的验证。
输入的值可以被捕获和监听`cancel`事件。

### 全局方法

可以使用 `alert()`方法，来直接显示alert dialog。（不必显示在代码中：`Ti.UI.createAlertDialog()`)。

有个全局的方法:`alert()` 被可以当做alert dialog的对象，它是只有一条文本信息的对话框。

例如：
```javascript
alert('hello world ！');
```

这样生成的对话框会带有一个写着‘Alert’的标题和一个写着‘OK’的按钮。

### 注意

一次不应该显示多个对话框!

`title`和`ok`属性值不能在对话框已经显示之后再来改变。只有在Andorid上，
你才能在对话框已经被显示之后修改`message`的值。

## 各种类型的alert dialog

### 单按钮对话框（快捷版）

使用`alert()`创建一个单按钮对话框

```javascript
Ti.UI.setBackgroundColor('white');
var win = Ti.UI.createWindow({
  title: 'Click window to test',
  backgroundColor: 'white',
  exitOnClose: true,
  fullscreen: false
});

win.addEventListener('click', function(e){
  alert('我是个alert dialog!');
});
win.open();
```

### 单按钮对话框（标准版）
创建一个没有预先定义赋值给`buttonNames`的对话框，点击window时，显示该对话框。

```javascript
Ti.UI.setBackgroundColor('white');
var win = Ti.UI.createWindow({
  title: '点击我来测试',
  backgroundColor: 'white',
  exitOnClose: true,
  fullscreen: false
});

win.addEventListener('click', function(e){
  var dialog = Ti.UI.createAlertDialog({
    message: '我是个标准版的alert dialog',
    ok: '确定',
    title: '标题'
  });
  dialog.show();
});
win.open();
```

### 三个按钮的对话框

创建一个有三个按钮的对话框，当点击window时被显示，并且在取消按钮被点击时，
在日志中输出一条信息。

```javascript
Ti.UI.setBackgroundColor('white');
var win = Ti.UI.createWindow({
  title: '点击我来测试',
  backgroundColor: 'white',
  exitOnClose: true,
  fullscreen: false
});
win.addEventListener('click', function(e){
  var dialog = Ti.UI.createAlertDialog({
    cancel: 1,
    buttonNames: ['确认', '取消', 'Help'],
    message: '要删除这个文件吗?',
    title: 'Delete'
  });
  dialog.addEventListener('click', function(e){
    if (e.index === e.source.cancel){
      Ti.API.info('您点击了 取消 按钮');
    }
  });

  dialog.show();
});
win.open();
```

### 允许输入简短文本的对话框

这种对话框只支持iOS 5以及更高的版本。

创建一个允许用户输入简单文本的对话框，点击window时显示，并且在点击ok按钮时，
在日志中输入用户输入的值。

```javascript
Ti.UI.setBackgroundColor('white');

var win = Ti.UI.createWindow({
  title: '点击我来测试'
});

win.addEventListener('click', function(e){
  var dialog = Ti.UI.createAlertDialog({
    title: '请输入文字',
    style: Ti.UI.iPhone.AlertDialogStyle.PLAIN_TEXT_INPUT,
    buttonNames: ['确定']
  });
  dialog.addEventListener('click', function(e){
    Ti.API.info('e.text: ' + e.text);
  });
  dialog.show();
});
win.open();
```

