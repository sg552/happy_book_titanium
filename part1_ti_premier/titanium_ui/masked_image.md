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

创建MaskedImage的时候有两个属性**mask**/**image**我们要特别注意。因为这两个属性并不由它们本身的含义
来确定两张需要处理的图片的“**渲染层**masked”和“**被渲染层**image”之间的关系，它们之间渲染逻辑的关系
最终是由**渲染的方式mode**来确定的，不同的渲染方式确定了它们的渲染层关系。例如：如果渲染方式mode使
用的是**BLEND_MODE_SOURCE_OUT**，那么此时mask是**alpha渲染层**会作为**_background/destination image_**，
imge则是**被渲染层**会作为**_foreground/source image_**，章节开始给出的参考代码就是这种情况。由此可见，
mask/image之间的逻辑渲染关系最终需要渲染方式mode来最终确定，甚至在一些特殊的渲染模
式下是不需要image属性的(如**BLEND_MODE_LUMINOSITY**模式只需要mask和tint属性)。

Titanium提供了多种多样的渲染模式，这使得MaskedImage的效果也丰富多彩！这里我们不再进行这些效果具体描述，
需要更多的参考样例请参考以下链接：
https://developer.apple.com/library/ios/documentation/GraphicsImaging/Conceptual/drawingwithquartz2d/dq_images/dq_images.html#//apple_ref/doc/uid/TP30001066-CH212-TPXREF101
