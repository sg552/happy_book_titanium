Welcome to iOS specific UI world！

iOS和Android都有特定于自己platform的特性，下面简单介绍以下特定于iOS平台的一些UI方面的特点。

### iPad-only UI APIs

iPad有两个特定的UI组件，是iPhone上都没有的。
- Popover
- Splitwindow

### popover就是在你点击某一个UI component时，会弹出一个悬浮的View

```javascript
var button = Ti.UI.createButton({
title: "Show popover",
width: 250,
height: 50,
top: 30,
right: 5
});

var popover = Ti.UI.iPad.createPopover({
width: 300,
height: 250,
title: 'I'm a Popover',
arrowDirection: Ti.UI.iPad.POPOVER_ARROW_DIRECTONI_RIGHT
});

button.addEventListener("click", function() {
popover.show({
view: button, // 这一行很关键，建立了button和popover的关系
animated: true
});
});
win.add(button);
```
### SplitWindow是分屏操作的UI组件（iPhone可能已经支持了）

SplitWindow由三部分组成：
- SplitWindow
- masterWindow
- detailWindow

SplitWindow包含了masterWindow和detailWinow，detailWinow是在点击masterWindow的时候，显示的具体的内容
```javascript
var masterWindow = Ti.UI.createWindow({
backgroundColor: "#fff"
})

masterWindow.add(Ti.UI.createLable({
text: "Master View",
top: 10,
height: 'Ti.UI.SIZE',
font:{
textAlign: "center",
fontSize: "bold"
}
}));

var detailWindow = Ti.UI.createWindow({
backgroundColor: "#dfdfdf"
})

detailWindow.add(Ti.UI.createLable({
text: "Detail View",
top: 10,
height: 'Ti.UI.SIZE',
font:{
textAlign: "center",
fontSize: "bold"
}
}));

var splitWindow = Ti.UI.iPad.createSplitWindow({
detailView: detailWindow,
masterView: masterWindow,
orientionModes: [Ti.UI.LANDSCAPE_LEFT, Ti.UI.LANDSCAPE_RIGHTE]
});

splitWindow.open();
```

### Badges

Badges就是手机上用来提示跟新或者消息的那个小红点。是iOS特有的UI。

下面通过代码，简单讲解如何使用这个UI组件。
```javascript
// 设置整个app的badge
Ti.UI.iPhone.appBadge = 23;

var tabGroup = Ti.UI.createTabGroup();
var win1 = Ti.UI.createWindow({
title: "window 1",
backgroundColor: "#fff"
});

var tab1 = Ti.UI.createTab({
icon: "KS_nav_views.png",
title: "Tab 1",
window: win1,
badger: 10 // 设置tab的提示的数量
});
```
