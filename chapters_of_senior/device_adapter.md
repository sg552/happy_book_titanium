# 适配不同机型和屏幕

最初开发Titanium的时候，我们在适配问题上耗费了大量的时间。如果一个一个机型，平台
去适配的话，占的时间大约是开发时间的70%。安卓跟ios不一样，不同尺寸的屏幕效果
也不一样。

后来遇到了刘明星，他的解决方案非常犀利:

- 不适用dp, pix 这样固定的尺寸单位。
- 针对不同的屏幕算出一个值，作为屏幕尺寸，几乎等同于缩放。

## 经典模式的解决方案。

来自于明星框架.

在alloy.js中定义一个全局的方法: unit()

```javascript
Ti.App.platform_height = Titanium.Platform.displayCaps.platformHeight
Ti.App.logicalDensityFactor = Titanium.Platform.displayCaps.logicalDensityFactor

function unit(x){
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

然后就可以调用了：

```javascript
var label1 = Ti.UI.createLabel({
  color: '#900',
  text: 'A simple label',
  width: unit(100),
  height: unit(100)
})
```

记得要删除`tiapp.xml`里面的默认单位配置

```xml
<!-- 删掉这行 -->
<property name="ti.ui.defaultunit" type="string">dp</property>
```

这时候的不同屏幕大小的`android`、`ios`或`ipad`的适配就差别就不太大了。


## Alloy下的解决方案

### 适配不同的机型

在tss文件里面定义一个label的样式

默认的label:

```css
"Label": {
    backgroundColor: "#000",
    text: 'BlackBerry or another platform'
},
```

iPhone下的label:

```css
"Label[platform=ios formFactor=handheld]": {
     backgroundColor: "#f00",
     text: 'iPhone'
  },
```
iPad和iPad mini:

```css
"Label[platform=ios formFactor=tablet]": {
     backgroundColor: "#0f0",
     text: 'iPad'
  },
```
黑莓机型和mobileweb端:

```css
"Label[platform=blackberry,mobileweb]":{
     text: 'blackberry and mobile web'
  },
```
如果不是ios:

```css
  "Label[platform=!ios]":{
     text: "I am not ios!"
  }
```

但注意以下几点:

- "Label"与"[platform" 之间，不能有空格！
- platform 可选的值，是android, ios, blackberry, mobileweb
- formFactor 表示作用于 `phone(=handheld)` 还是pad `(=tablet)`,
- 多个平台，可以使用 platform=android,ios
- 如果不希望作用于某个平台，使用！， 例如： platform=!ios

### 适配不同的版本

首先在alloy.js中定义相关的版本号

```css
Alloy.Globals.isIos7Plus = (OS_IOS && parseInt(Ti.Platform.version.split(".")[0]) >= 7);

Alloy.Globals.iPhoneTall = (OS_IOS && Ti.Platform.osname == "iphone" && Ti.Platform.displayCaps.platformHeight == 568);
```

然后就可以根据不同的版本号来做判断了。

```
"Label[if=Alloy.Globals.isIos7Plus]":{
  text: "只在ios7+的版本上显示的消息"
}
```
