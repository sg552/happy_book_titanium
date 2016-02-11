###Animation Style
animation style为在不同窗口间转换时的过渡效果。主要有五中过渡效果：
* CURL_DOWN：向下卷动
* CURL_UP：向上卷动
* FLIP_FROM_LEFT：从左向右翻转
* FLIP_FROM_RIGHT：从右往左翻转
* NONE：没有动画效果

动画效果示例：

CURL_DOWN:

![CURL_DOWN](http://image.tidev.in/image/204/curl_down.gif)

CURL_UP:

![CURL_UP](http://image.tidev.in/image/205/curl_up.gif)

FLIP_FROM_LEFT:

![FLIP_FROM_LEFT](http://image.tidev.in/image/206/flip_from_left.gif)

FLIP_FROM_RIGHT:

![FLIP_FROM_RIGHT](http://image.tidev.in/image/207/flip_from_right.gif)


四种动画效果可以在很多的UI组件中使用，包括`view`,`window`
```javascript
//在给view中的butten_bar指定从左向右的卷动效果
view.animate({view:butten_bar,transition:Ti.UI.iPhone.AnimationStyle.FLIP_FROM_LEFT});
//在窗口的打开过程中指定向上卷动的动画效果
window.open({transition:Ti.UI.iPhone.AnimationStyle.CURL_UP});
```
