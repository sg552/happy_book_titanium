# MaskedImage

MaskedImage是一个类似于ImageView并为图片添加渲染效果功能的UI组件，
正如其名“戴面具的图片”；

因此它能对图片进行一些简单的渲染处理，如：为图片添加类似相框的效果，
如果图片背景透明可以为图片 添加自定义的背景图，

或者将两张图片进行alpha融合等。

这个组件还是比较专业的，一般来说我们用不到。

原图：

![logo](/images/ui_masked_image_before.png)

使用绿色进行 luminosity 渲染后：

![result](/images/ui_masked_image_result.png)


源代码如下：
```js
Ti.UI.backgroundColor = 'white';
var win = Ti.UI.createWindow();

var image_mask= Titanium.UI.createMaskedImage({
  mask : '/images/bdlogo.png',
  tint: 'green',
  mode : Titanium.UI.iOS.BLEND_MODE_LUMINOSITY,
  height: 400,
  width: 500
});

win.add(image_mask);
win.open()
```

创建MaskedImage时, 对于'BLEND_MODE_SOURCE_OUT' 有两个属性要特别注意:
mask, image。
因为这两个属性并不由它们本身的含义来确定两张需要处理的图片的
“渲染层masked”和“被渲染层image”之间的关系，它们之间渲染逻辑的关系
最终是由渲染的方式mode来确定的，不同的渲染方式确定了它们的渲染层关系。

例如：如果渲染方式mode使用的是BLEND_MODE_SOURCE_OUT，那么此时mask是
alpha渲染层会作为_background/destination image_，
image则是被渲染层会作为_foreground/source image_，
章节开始给出的参考代码就是这种情况。

由此可见， mask/image之间的逻辑渲染关系最终需要渲染方式mode来最终确定，
甚至在一些特殊的渲染模 式下是不需要image属性的(如BLEND_MODE_LUMINOSITY
模式只需要mask和tint属性)。

Titanium提供了多种多样的渲染模式，这使得MaskedImage的效果也丰富多彩！
这里我们不再进行这些效果具体描述，

需要更多的参考样例请参考以下链接：

https://developer.apple.com/library/ios/documentation/GraphicsImaging/Conceptual/drawingwithquartz2d/dq_images/dq_images.html#//apple_ref/doc/uid/TP30001066-CH212-TPXREF101
