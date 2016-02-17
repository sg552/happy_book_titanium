# 自动适配多种不同机型和屏幕

靠下面这段代码实现：

```js
function __l(x){
  if (Ti.App.is_android){
    if (Ti.App.platform_height/Ti.App.logicalDensityFactor > 800)
      return x * Ti.App.logicalDensityFactor * 1.4;
    else
      return x * Ti.App.logicalDensityFactor;
  }
  if (!Ti.App.is_android && !Ti.App.is_ipad && Ti.App.platform_width > 320){
    return parseInt(375.0*x/320);
  }
  return Ti.App.is_ipad ? 1.5*x : x;
}
```
这个代码的作用不是简单的按百分比缩放，而是在某范围内的屏幕下有个特定的尺寸，
在另一个范围内的屏幕尺寸下，再有个特定的尺寸。

使用方式：

```js
Ti.UI.createLabel({
  width: __l(50);
});
```
