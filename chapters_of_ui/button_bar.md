# Titanium.UI.ButtonBar(Only IOS)

多个Button组成的 Button组。

![ButtonBar](/images/ui_button_bar.png)

## 使用

```javascript
var buttonbar = Titanium.UI.createButtonBar({
    labels:['One', 'Two', 'Three'],
    backgroundColor:'#777',
    top:50,
    style:Titanium.UI.iPhone.SystemButtonStyle.BAR,
    height:25,
    width:200
});
win.add(buttonbar);
```


