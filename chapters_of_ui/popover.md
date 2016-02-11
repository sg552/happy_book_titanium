# Popover

提示框。

合理的使用提示框，可以起到意想不到的好效果。

![popover](/images/ui_ipad_popover.gif)

# 例子

```js
var win = Ti.UI.createWindow({backgroundColor: 'white'});

var button = Ti.UI.createButton({title: '我是触发popover的button, 离开我就没有popover!'});
button.addEventListener('click', function(e){
    popover.show({ view: button });
})
win.add(button);

var rightButton = Ti.UI.createButton({title: '其他信息'});
rightButton.addEventListener('click', function(e){
    alert("学完Titanium 务必要学习Ruby on Rails.");
});

var contentWindow = Ti.UI.createWindow({
    rightNavButton: rightButton,
    title: '你好！我是contentView',
    width: 250,
    height: 100
});
contentWindow.add(Ti.UI.createLabel({text: "我是contentView的正文"}));

var popover = Ti.UI.iPad.createPopover({
    width: 250,
    height: 100,
    backgroundColor: 'green',
    contentView: Ti.UI.iOS.createNavigationWindow({window: contentWindow})
});

win.open();
```

