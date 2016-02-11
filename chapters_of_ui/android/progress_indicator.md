#ProgressIndicator

这里讲的ProgressIndicator是Android独有的特征，只作用在Android上。所以它的命名空间就是`Titanium.UI.Android.ProgressIndicator`。
它的作用是通过一个UI效果来显示一个正在运行的进程，以此来告诉用户当前这个进程运行的进度。

##使用方法
+ 在js文件中，通过`Titanium.UI.Android.createProgressIndicator`方法
+ 在Alloy框架中的xml文件中，使用`<ProgressIndicator>`元素标签对
+ progress indicator 可以当作一个进度对话框（progress dialog）也可以在一个window的上方当作一个水平进度条。
+ 通过`show()`方法来调用显示这个进度条，通过`hide()`来移除它。

##使用例子
###在js文件中实现显示一个进度条，并且执行完一些代码之后关闭它。
```javascript
Ti.UI.backgroundColor = 'white';

var win = Ti.UI.createWindow({
  backgroundColor: 'blue'
});

var button = Ti.UI.createButton({
  title: 'Show Progress Dialog'
});

var progressIndicator = Ti.UI.Android.createProgressIndicator({
  message: 'Loading...',
  location: Ti.UI.Android.PROGRESS_INDICATOR_DIALOG,
  type: Ti.UI.Android.PROGRESS_INDICATOR_DETERMINANT,
  cancelable: true,
  min: 0,
  max: 10
});

button.addEventListener('click', function (e) {
    progressIndicator.show();
    var value = 0;
    setInterval(function(){
      if (value > 10) {
      return;
      }
      progressIndicator.value = value;
      value ++;
      }, 200);
    // do some work that takes 3 seconds
    // ie. replace the following setTimeout block with your code
    setTimeout(function(){
      progressIndicator.hide();
      }, 3000);
    });

win.add(button);
win.open();
```
显示效果：
![ProgressIndicator](http://image.tidev.in/image/31/屏幕快照 2015-09-06 下午3.26.37.png)

###在Alloy中实现如上效果

index.xml:
```xml
<Alloy>
    <Window backgroundColor="blue">
        <Button id="button" onClick="showIndicator">Show Progress Dialog</Button>

        <ProgressIndicator ns="Ti.UI.Android" platform="android" id="progressIndicator"
        message="Loading..." min="0" max="10" cancelable="true"
        location="Ti.UI.Android.PROGRESS_INDICATOR_DIALOG"
        type="Ti.UI.Android.PROGRESS_INDICATOR_DETERMINANT" />
    </Window>
</Alloy>
```

index.js:
```javascript
function showIndicator(e) {
  $.progressIndicator.show();
  var value = 0;
  setInterval(function(){
      if (value > 10) {
      return;
      }
      $.progressIndicator.value = value;
      value ++;
      }, 200);
  // do some work that takes 3 seconds
  // ie. replace the following setTimeout block with your code
  setTimeout(function(){
      $.progressIndicator.hide();
      }, 3000);
}
$.index.open();
```
