#Gestures(手势)
除去一些简单的点击操作，我们在实际使用应用的时候，会用到很多的手势操作（例如：摇手机，滑动等）来增加我们和应用交互上的便捷性和体验好感。Titanium自然也提供很多常用的手势API，供我们来优化我们的APP。

##以下是一些常用的手势
+ Shake(摇一摇)
+ Swipe(滑动)
+ Touch(触摸)
+ Pinch(手指缩放)
+ Long press(长按)
+ Accelerometer(加速器)

*官方提供手势其实是一个官方的module。所以我们可以通过`Ti.Gesture`这个module来实现我们的需求。*

###Shake（摇一摇）
```javascript
Ti.Gesture.addEventListener('shake',function(e) {
    alert('shaken at '+e.timestamp);
});
```
e.timestamp是事件的时间戳，我们可以利用这个时间戳的参数来判断手机被摇晃的时间。在iOS simulator 上测试的时候是在HardWare中点击Shake Gestures。Android中的虚拟机是不支持shake的，可以用真机设备测试。

iOS的效果：
![ios shake](http://image.happysoft.cc/image/66/屏幕快照 2015-09-08 下午3.04.06.png)

Android的效果：
![android shake](http://image.happysoft.cc/image/67/1.pic_hd.jpg)

###Swipe（滑动）
Swipe是指用手指左右拖拽滑动。
```javascript
$.index.addEventListener('swipe', function(e) {
    if (e.direction == 'left') {
    alert('You swiped to the left ');
    } else if (e.direction == 'right') {
    alert('You swiped to the right');
    }
    });
$.index.open();
```

iOS效果如图：
![](http://image.happysoft.cc/image/72/屏幕快照 2015-09-08 下午3.44.24.png)

Android效果如图：
![](http://image.happysoft.cc/image/73/3.pic_hd.jpg)

###Touch
Touch不能单独来谈，要结合Titanium UI组件来用。Touch事件可以细分为四个事件。
+ touchstart --当用户的手指第一次触碰到设备的屏幕的时候被触发
+ touchend --当用户把手指拿起离开手机屏幕的时候被触发
+ touchmove --当用户连续的用手指在屏幕上滑动拖拽时被触发
+ touchcancel --当一个操作系统的事件来打断了一个正在持续进行的touch事件时，比如突然来电，时被触发

事件对象只有两个属性是有用的：x和y的坐标。我们可以通过这个来追踪用户在使用程序时的手势经历。
在Android中，其他事件例如long press ，swipe之类的是不能在touchstart事件之后被触发。

###Pinch
Titanium目前只支持iOS。
```javascript
$.index.addEventListener('pinch', function(e){
    alert('You pinched to ' + e.scale*100 + '%');
    });
$.index.open();
```
iOS效果如图：
![pinch ios](http://image.happysoft.cc/image/71/屏幕快照 2015-09-08 下午4.25.42.png)

###Long press（长按）
```javascript
$.index.addEventListener('longpress', function(e){
    alert('You pressed at coordinates ' + e.x + ' / ' + e.y);
});
$.index.open();
```

iOS效果如图：
![](http://image.happysoft.cc/image/74/屏幕快照 2015-09-08 下午5.07.02.png)

Android效果如图：
![](http://image.happysoft.cc/image/75/屏幕快照 2015-09-08 下午5.12.08.png)

###Accelerometer
Accelerometer是作为一个硬件单元集成在机设备中，当设备发生移动，是会返回一个新的三维空间中的位置。它只有一个事件，叫`update`。这个module暴露出这个接口来输出位置信息。
Accelerometer需要打开开关以便能反馈给操作系统，因为消耗太多的能量的话，就会慢慢的把电池电量给用完，所以一般推荐在不使用的情况下不打开开关。
Accelerometer在安卓中是通过暂停和恢复应用来关闭和开启开关。
```javascript
$.index.setLayout('vertical');
opts = {
  color:'black',
  font:{fontSize:20},
  text:'-',
  top:20, left:10,
  width:300
};
var labelTimestamp = Ti.UI.createLabel(opts);
$.index.add(labelTimestamp);
var labelx = Ti.UI.createLabel(opts);
$.index.add(labelx);
var labely = Ti.UI.createLabel(opts);
$.index.add(labely);
var labelz = Ti.UI.createLabel(opts);
$.index.add(labelz);

var accelerometerCallback = function(e) {
  labelTimestamp.text = 'timestamp: ' + e.timestamp;
  labelx.text = 'x: ' + e.x;
  labely.text = 'y: ' + e.y;
  labelz.text = 'z: ' + e.z;
};

if (Ti.Platform.model === 'Simulator' || Ti.Platform.model.indexOf('sdk') !== -1 ){
  alert('Accelerometer does not work on a virtual device');
} else {
  Ti.Accelerometer.addEventListener('update', accelerometerCallback);
  if (Ti.Platform.name === 'android'){
    Ti.Android.currentActivity.addEventListener('pause', function(e) {
        Ti.API.info("removing accelerometer callback on pause");
        Ti.Accelerometer.removeEventListener('update', accelerometerCallback);
        });
    Ti.Android.currentActivity.addEventListener('resume', function(e) {
        Ti.API.info("adding accelerometer callback on resume");
        Ti.Accelerometer.addEventListener('update', accelerometerCallback);
        });
  }
}
$.index.open();
```

Android效果如图：
![](http://image.happysoft.cc/image/76/屏幕快照 2015-09-09 上午10.05.11.png)

###事件管理与生命周期
Android是一个多任务处理的环境，所以当app被挂起或者暂停时，移除一些全局事件就显得很重要了。如果你不这么做的话，硬件的所支持的那些全局事件就不会一直被触发，一直保持这个状态。移除事件监听会有利于限制电池电量被设备组件浪费。为了移除监听事件，你必须传递`addEventListener()`同样的`function signature`给`removeEventListener()`。例子同上！


