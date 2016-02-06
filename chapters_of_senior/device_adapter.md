# 不同机型的适配

##关于机型适配你必须知道的技巧

  众所周知，移动端的开发都会有一个很棘手的问题，这个问题就是不同机型的适配。作为开发人员，大量的时间可以专注在业务的处理和产品的评估上，那么机型适配我们必然要有一个很好的解决方案。Titanium作为跨平台开发技术，机型的适配必然是一个痛点也是重点
以下就是我们公司在机型适配上采取的两种相对高效和可以解放大量生产力的方法。大部分Titanium使用了Alloy框架，Alloy框架的使用，可以把复杂的逻辑转换成mvc这种简单的开发模式，但是同时也带来一定的适配问题，所以我们的方法是将样式全部写在tss文件中，不要在试图层嵌入大量的样式代码。这样会在机型适配和样式调整上都会带来大量的问题。将样式写在tss里面，我们用不同机型的Label适配为例:

##第一种方案:

###适配不同的机型

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

1. "Label"与"[platform" 之间，不能有空格！
2. platform 可选的值，是android, ios, blackberry, mobileweb
3. formFactor 表示作用于  phone(=handheld) 还是pad (=tablet),
4. 多个平台，可以使用 platform=android,ios
5. 如果不希望作用于某个平台，使用！， 例如： platform=!ios


###适配不同的版本

首先在alloy.js中定义相关的版本号

```css
Alloy.Globals.isIos7Plus = (OS_IOS && parseInt(Ti.Platform.version.split(".")[0]) >= 7);

Alloy.Globals.iPhoneTall = (OS_IOS && Ti.Platform.osname == "iphone" && Ti.Platform.displayCaps.platformHeight == 568);
```

##第二种方案:
第一种方案可以解决部分方案，我们还有第二种方案可以解决机型适配，能够花较少的时间用在适配当中来

- 在alloy.js中定义一个全局的方法

```javascript
Ti.App.platform_height = Titanium.Platform.displayCaps.platformHeight
Ti.App.logicalDensityFactor = Titanium.Platform.displayCaps.logicalDensityFactor

function unit(x){
  if (Ti.App.is_android){
     if (Ti.App.platform_height/Ti.App.logicalDensityFactor > 800)
      return x * Ti.App.logicalDensityFactor * 1.4;
    else
      return x * Ti.App.logicalDensityFactor;
          
     //return parseInt(Ti.App.platform_width*x/(Ti.App.logicalDensityFactor == 1 ? 360 : 320));
  }
  if (!Ti.App.is_android && !Ti.App.is_ipad && Ti.App.platform_width > 320){
    return parseInt(375.0*x/320);
  } 
  return Ti.App.is_ipad ? 1.5*x : x;
}
```

- 在controller创建Label的时候使用`alloy.js`中定义方法来调整单位：

```javascript
var label1 = Ti.UI.createLabel({
  color: '#900',
  text: 'A simple label',
  width: unit(100),
  height: unit(100)
})
```
- 删除`tiapp.xml`里面的默认单位配置

```xml
 <property name="ti.ui.defaultunit" type="string">dp</property>
```
这时候的不同屏幕大小的`android`、`ios`或`ipad`的适配就差别就不太大了。