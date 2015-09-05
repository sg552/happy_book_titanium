# 不同机型的适配
##关于机型适配你必须知道的技巧

  众所周知，移动端的开发都会有一个很棘手的问题，这个问题就是不同机型的适配。作为开发人员，大量的时间可以专注在业务的处理
和产品的评估上，那么机型适配我们必然要有一个很好的解决方案。Titanium作为跨平台开发技术，机型的适配必然是一个痛点也是重点
以下就是我们公司在机型适配上采取的两种相对高效和可以解放大量生产力的方法。大部分Titanium使用了Alloy框架，Alloy框架的使用，
可以把复杂的逻辑转换成mvc这种简单的开发模式，但是同时也带来
一定的适配问题，所以我们的方法是将样式全部写在stss文件中，不要在试图层嵌入大量的样式代码。这样会在机型适配和样式调整上都会
带来大量的问题。将样式写在css里面，我们用不同机型的Label适配为例:

###第一种方案:

1)适配不同的机型

默认的label
```css
"Label": {
    backgroundColor: "#000",
    text: 'BlackBerry or another platform'
},
```


iPhone下的label
```css
"Label[platform=ios formFactor=handheld]": {
     backgroundColor: "#f00",
     text: 'iPhone'
  },
```


iPad和iPad mini
```css
"Label[platform=ios formFactor=tablet]": {
     backgroundColor: "#0f0",
     text: 'iPad'
  },
```


黑莓机型和mobileweb端
```css
"Label[platform=blackberry,mobileweb]":{
     text: 'blackberry and mobile web'
  },
```


如果不是ios
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


2)适配不同的版本

首先在alloy.js中定义相关的版本号

```css
Alloy.Globals.isIos7Plus = (OS_IOS && parseInt(Ti.Platform.version.split(".")[0]) >= 7);

Alloy.Globals.iPhoneTall = (OS_IOS && Ti.Platform.osname == "iphone" && Ti.Platform.displayCaps.platformHeight == 568);
```




###第二种方案:
第一种方案可以解决部分方案，我们还有第二种方案可以解决机型适配，真正做到0适配

在alloy.js中

```css

funciton adapter(device)
  {
   //全局的高度和宽度
    platformHeight = Titanium.Platform.displayCaps.platformHeight * Titanium.Platform.displayCaps.logicalDensityFactor
    platformWidth  = Titanium.Platform.displayCaps.platformWidth * Titanium.Platform.displayCaps.logicalDensityFactor

  if(OS_IOS == device){


  }
  if(OS_ANDROID == device){


  }
}

```