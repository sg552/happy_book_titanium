Welcome to Android Specific World!!!

一下简单介绍Titanium开发中，需要注意的特定于Android系统的UI组件。
- Action Bar
- Action Menu
- Back Button
- Lable
- Toast Notification
- Status Bar Notification
- Nine-Path Images

### Action Bar
Android的Action Bar是是一个Window的一部分，用来branding的，具体的内容，可以参考Android的官方文档。

### Android Menu
在原生的Android里面，每一个Activity，都有一个相应的menu。

在Titanium里面，每一个‘heavyweight’ Window都有自己的menu，而实际实际上，Titanium中的每一个heavywindo，对应Android里面的一个activity。

Android Menu，在Titanium中，是使用特定于Android的API写成。
比如像下面这样：
```javascript
activity = Ti.Android.currentActivity;
activity.createOptionsMenu = function(e) {
var menu = e.menu;
var menuItem = menu.add({title: "Item 1"});
menuItem.setIcon("item1.png");
menuItem.addEventListener("click", function(e) {...});
};

// 另一种写法
var win = Ti.UI.createWindow({
navBarHiden: false,
acitity: {
onCreateOptionsMenu: function(e) {
var menu = e.menu;
var menuItem = menu.add({ title: "Item 1"});
menuItem.setIcon("item1.png");
menuItem.addEventListener("click", function() {...});
}
}
});
```

### Android Back Button
Android Back Button，在很多Android机器上，是实体键，即hardware-specific。

作用是为了，销毁顶层Window，即stack of the open windows。
```javascript
var win = Ti.UI.createWindow({
title: "Hello, world",
backgroundColor: "#fff",
fullscreen: false
});

win.addEventListener("androidback", function() {});
```

### Android Label
Android的label可以使用HTML元素，需要注意的是，需要使用html这个property，而不是普通label的text这个property。

具体的实现代码如下：
```javascript
var label = Ti.UI.createLabel({
html: "This is a <b>HTML</b> <i>element</i>",
text: "This is for iOS",
top: 125,
height: 50,
width: '100%'
});
```

Android的text属性，如果property value是一个链接的话，会有类似web中点击一个link的体验。比如点击一个label的text的属性的property value是一个email link的话，会调用手机的email客户端；点击一个电话号码，会调用手机上的拨号键盘。

需要注意的是，这样使用的时候，需要加上另外一个特殊的property，`autoLink`。

具体的使用代码如下:
```javascript
var label = Ti.UI.createLabel({
autoLink: Ti.UI.AUTOLINK_ALL,
left: 5, top: 5, right: 5, height: 100,
backgroundColor: "#222",
text: "Contact\n test@test.com\n 010-888-8888\n http://www.huahua.world"
});
```

autoLink的属性的值有以下几个：
- Ti.UI.AUTOLINK_ALL, 将所有的link当做link看待，而不是文本，
- Ti.UI.AUTOLINK_EMAIL_ADDRESS, 仅仅将email的链接当做链接看待，其他的链接当做文本看待
- Ti.UI.AUTOLINK_MAP_ADDRESS, 仅仅处理map address
- Ti.UI.AUTOLINK_PHONE_NUMBERS, 仅仅处理电话
- Ti.UI.AUTOLINK_URLS, 仅仅处理web url，就是我们经常说的网址

### Toast Notification
Android可以有那种小的提示，出现一会儿，然后自动消息，用来输出提示信息的组件，
具体用法，看下面代码：
```javascript
var n = Ti.UI.createNotification({message: "Hello, world"});
n.duration = Ti.UI.NOTIFICATION_DURATION_LONG;
n.offsetX = 100;
n.offsetY = 75;
n.show();
```

### Status Bar Notification
Status Bar就是Android手机，最上面的那个状态栏，可以看电池的电量，是否连接上了WiFi，有没有新的微信消息。

在Titanium中可以创建这些特定于Android的UI。

具体的实现代码如下：

``javascript
// 就像intent(目的，意图)单词暗示的那样，intent在这里是声明你要要坐什么
var intent = Ti.Android.createIntent({
action: Ti.Android.ACTION_DIAL,
data: "tel: 15011112222"
});

var pending = Ti.Android.createPendingIntent({
activity: Ti.Android.currentActivity,
intent: intent,
type: Ti.Android.PENDING_INTENT_FOR_ACTIVITY,
flags: Ti.Android.FLAG_UPDATE_CURRENT
});

var notification = Ti.UI.createNotification({
icon: 0x7f020000,
contentTitle: "现在就打过去!",
contentText: "15011112222",
contentIntent: pending
});

Ti.Android.NotificationManager.notify(1, notification);
```
