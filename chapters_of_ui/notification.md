# Notification

Notification是消息通知UI组件，十分类似于AlertDialog；
但是它弹出消息的时候并不会锁定屏幕，而AlertDialog等对话框事件是会锁定屏幕的(锁定屏幕时，只能对当前对话框窗口进行
操作)。

另外，需要注意的是Notification只适用于Android和Windows Phone，平台十分有限；
除此之外Notification 在这两个平台上显示的区域也不相同，

Android上显示在靠近屏幕底部边缘位置，而在Windows Phone上Notification则
在消息通知栏上显示。

Notification的适用平台十分有限，但是却是个很好用的UI组件.

![notification](/images/notification_display.gif)

```js
var toast = Ti.UI.createNotification({
  message: "显示",
  duration: Ti.UI.NOTIFICATION_DURATION_LONG
});
toast.show();
```

演示案例通过点击“查看消息”button来显示Notification，
这只是为了简便展示Notification的UI效果，实际情况下Notification
应该通过事件驱动来调用当某个事件发生后，如果需要对用户进行消息提示，
那么就调用Notification把消息展示给用户；
这种事件驱动有很多，如：下载完成提示，新接收的短信消息等等。
这些地方都可以用到Notification。

除此之外Notification还有一个不好的缺点，那就是它无法进行样式调整；如:
想要改变Notification的背景色，正文，字体的大小或颜色等等；
唯一能改变的就是消息显示时间的长短，即Notification的存在时间(duration)，
在演示案例里我们设置为长时间的显示
(`duration:Ti.UI.NOTIFICATION_DURATION_LONG`)，
默认是为短时间显示(`duration: Ti.UI.NOTIFICATION_DURATION_SHORT`)。

Notification可自定义样式的限制比较多，如果对它十分感兴趣的同学建议去看看
原生Android中的Notification机制，然后再通过Widget的介绍可以自定义出一个适合自己
的Notification。以下是给出的一些建议网址：

1.IOS本地设置Notification：

http://docs.appcelerator.com/platform/latest/#!/guide/iOS_Local_Notifications

2.开源中国Android源生Notification：

http://www.oschina.net/question/234345_40111

3.Titanium Notification Widget参考：

http://gitt.io/component/com.caffeinalab.titanium.notifications
