# Titanium.UI.Clipboard(剪切板)

> TODO 这个没用过

先贴个官方文档的代码例子：


```javascript
Ti.API.log('Deleting all text in Clipboard');
Ti.UI.Clipboard.clearText();
Ti.API.log('Clipboard.getText(): ' + Ti.UI.Clipboard.getText()); // returns empty string on Android and undefined on iOS
Ti.API.log('Set text Clipboard to hello');
Ti.UI.Clipboard.setText('hello');
Ti.API.log('Clipboard.hasText(), should be true: ' + Ti.UI.Clipboard.hasText()); // returns true on Android and 1 on iOS
Ti.API.log('Clipboard.getText(), should be hello: ' + Ti.UI.Clipboard.getText());

```

* Clipboard是一个临时的储存空间,是一个single item of data能够在不同的app之间进行复制he粘贴。 
