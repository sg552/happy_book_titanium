#MaskedImage
**MaskedImage**是一个类似于ImageView并为图片添加渲染效果功能的UI组件，正如其名“戴面具的图片”；
因此它能对图片进行一些简单的渲染处理，如：为图片添加类似相框的效果，如果图片背景透明可以为图片
添加自定义的背景图，或者比较高级的将两张图片进行alpha融合等等。这个UI组件目前只适用于IOS平台。

MaskedImage不能通过静态定义声明，即不能在.xml文件中进行定义，只能使
用**Titanium.UI.createMaskedImage**的方法在.js文件中动态创建。以下是参考代码：

```js
var imageMask = Titanium.UI.createMaskedImage({
    mask : 'mask.png',
    image : 'demo_image.png',
    mode : Titanium.UI.iOS.BLEND_MODE_SOURCE_OUT
});
```

创建MaskedImage的时候有两个属性**mask**/**image**我们要特别注意。

详细的介绍和使用方法：
https://developer.apple.com/library/ios/documentation/GraphicsImaging/Conceptual/drawingwithquartz2d/dq_images/dq_images.html#//apple_ref/doc/uid/TP30001066-CH212-TPXREF101
