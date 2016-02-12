# ProgressIndicator

告诉用户当前这个进程运行的进度。

![ProgressIndicator](http://image.tidev.in/image/31/屏幕快照 2015-09-06 下午3.26.37.png)


## 例子

实现显示进度条，每300毫秒进度增加5，直到100.

![android](/images/ui_progress_indicator.gif)

```js

var win = Ti.UI.createWindow({backgroundColor: 'white'});

var progress_indicator = Ti.UI.Android.createProgressIndicator({
  message: '加载中...',
  location: Ti.UI.Android.PROGRESS_INDICATOR_DIALOG,
  type: Ti.UI.Android.PROGRESS_INDICATOR_DETERMINANT,
  cancelable: true,
  min: 0,
  max: 100
});

win.open();
progress_indicator.show();

var value = 0
setInterval(function(){
  progress_indicator.value = value;
  value = value + 5;
}, 300);
```

