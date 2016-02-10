# Titanium.UI.Clipboard(剪切板)

剪切板是个临时的空间，用来保存用户刚才复制的内容。

剪切板仅支持文本内容。

## 例子

```js
Ti.API.log('即将清空剪切板');
Ti.UI.Clipboard.clearText();
// 安卓机上是空， ios 上返回 undefined
Ti.API.log('Clipboard.getText(): ' + Ti.UI.Clipboard.getText());

Ti.API.log('把剪切板的内容变成 hello ');
Ti.UI.Clipboard.setText('hello');

// 安卓上返回true, ios上返回 1
Ti.API.log('Clipboard.hasText(), should be true: ' + Ti.UI.Clipboard.hasText());

// 两个平台都返回hello
Ti.API.log('Clipboard.getText(), should be hello: ' + Ti.UI.Clipboard.getText());
```

