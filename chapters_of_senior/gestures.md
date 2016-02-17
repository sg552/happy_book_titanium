# Gestures 手势

我们在实际使用应用的时候，会用到很多的手势操作
（例如：摇手机，滑动等）来提升用户体验。

Titanium提供了很多常用的手势API供我们使用。

注意：测试的时候要使用真机。

## 常用的手势

- Shake(摇一摇)
- Swipe(滑动)
- Touch(触摸)
- Pinch(手指缩放)
- Long press(长按)
- Accelerometer(加速器)

我们可以通过`Ti.Gesture`这个module来实现我们的需求。

## 摇一摇

```javascript
Ti.Gesture.addEventListener('shake',function(e) {
    alert('shaken at '+e.timestamp);
});
```
e.timestamp是事件的时间戳，我们可以利用这个时间戳的参数来判断手机被摇晃的时间。

效果：
![ios shake](/images/senior_shaken_ios.png)

(以后几个事件的效果类似, 图片略)

## 滑动

Swipe是指用手指左右拖拽滑动。

```javascript

window.addEventListener('swipe', function(e) {
  if (e.direction == 'left') {
    alert('You swiped to the left ');
  } else if (e.direction == 'right') {
    alert('You swiped to the right');
  }
});
```

## 触摸

Touch事件可以细分为四个事件:

- touchstart --当用户的手指第一次触碰到设备的屏幕的时候被触发
- touchend 当用户的手指离开屏幕的时候被触发
- touchmove 当用户手指在屏幕上滑动时被触发
- touchcancel 当一个操作系统的事件来打断了一个正在持续进行的touch事件时被触发，
比如突然来了个电话

事件对象只有两个属性是有用的：x和y的坐标。我们可以通过这个来追踪用户在使用
程序时的手势经历。

在Android中，其他事件例如long press ，swipe之类的是不能在touchstart
事件之后被触发。

## 双指缩放操作(Pinch)

只支持iOS。

```javascript
window.addEventListener('pinch', function(e){
  alert('You pinched to ' + e.scale*100 + '%');
});
```

## 长按

```javascript
window.addEventListener('longpress', function(e){
  alert('You pressed at coordinates ' + e.x + ' / ' + e.y);
});
```

## Accelerometer

Accelerometer是作为一个硬件单元集成在机设备中，当设备发生移动，
会返回一个新的三维空间中的位置。

它只有一个事件，叫`update`。这个module暴露出这个接口来输出位置信息。

Accelerometer需要打开开关，才能反馈结果给操作系统，因为消耗太多的能量的话，
就会慢慢的把电池电量给用完，所以在不使用的情况下，不要打开开关。

```javascript

var accelerometerCallback = function(e) {
  labelTimestamp.text = 'timestamp: ' + e.timestamp;
};

Ti.Accelerometer.addEventListener('update', accelerometerCallback);
if (Ti.Platform.name === 'android'){
  Ti.Android.currentActivity.addEventListener('pause', function(e) {
    Ti.Accelerometer.removeEventListener('update', accelerometerCallback);
  });
  Ti.Android.currentActivity.addEventListener('resume', function(e) {
    Ti.Accelerometer.addEventListener('update', accelerometerCallback);
  });
}
```

## 事件管理与生命周期

当app被挂起或暂停时，记得移除事件。否则app会一直耗电。


