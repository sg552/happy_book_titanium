# TextField

单行输入框，是使用最广泛的输入组件。

![android](/images/ui_textfield_android.png)| ![ios](/images/ui_textfield_ios.png)| ![wp](/images/ui_textfield_wp.png)|
:---:|:---:|:---:
Android|iOS|Windows Phone


## 基本用法

![basic](/images/ui_textfield.png)

```
var win = Ti.UI.createWindow({backgroundColor: 'white'});

var text_field = Ti.UI.createTextField({
  borderStyle: Ti.UI.INPUT_BORDERSTYLE_ROUNDED,
  borderWidth: 2,
  color: '#336699',
  top: 100,
  width: 400,
  height: 60
});

win.add(text_field);
win.open();
```

## 重要属性

- value

当前输入的值

- passwordMask

设置成密码输入框。用户看不到刚才输入的内容。效果如下图：

![password](/images/ui_textfield_password.png)

默认：false

- editable

是否可编辑。 默认是true.

- color

输入的字体的颜色。

- hintText

文字提示。

- inputType

要输入的是文字还是数字。可用的值是：

  - Ti.UI.INPUT_TYPE_CLASS_NUMBER   数字
  - Ti.UI.INPUT_TYPE_CLASS_TEXT  文字

- keyboardType

选择键盘。可用的值有很多，包括：

  - Ti.UI.KEYBOARD_TYPE_EMAIL 邮件键盘
  - Ti.UI.KEYBOARD_TYPE_DEFAULT 默认键盘

等等。具体用哪个请自行查阅API。

## 重要的事件

- blur: 焦点发生了变化

- focus: 焦点放在了这里

- change: 内容发生了变化

- return: 用户输入了 return
