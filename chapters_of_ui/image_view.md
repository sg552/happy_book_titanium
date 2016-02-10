# ImageView

一个展示图片或动态图片的组件,静态图片支持android里面的Nine-patch和Draw 9-patch图片文件。

加载中与加载完毕：

![加载中](/images/ui_imageview_uubpay_loading.png)
![加载完](/images/ui_imageview_uubpay_mobile.png)

## 基本的图片组件创建示例

```javascript
Ti.UI.backgroundColor = 'white';
var win = Ti.UI.createWindow();
var image = Ti.UI.createImageView({
  image:'/images/uubpay_mobile.png'
});
win.add(image);
win.open();
```

## 注意
- 如果你用的是alloy, 则`//image:'/images/uubpay_mobile.png'`
这行代码中的文件路径实际在项目
中的位置是*app/assets/images/uubpay_mobile.png*,
在使用`image`属性的时候不需要加上 *app/assets*路径。
- 在不指定宽高的情况下android上面的图片展示样式和ios有区别。
- 在android上面部分机型对图片的宽高有最大值限制。

## 设置默认的图片

使用 `defaultImage` 属性：

```js
var image = Ti.UI.createImageView({
  image:'/images/uubpay_mobile.png'
  defaultImage: '/images/default.png'
});
```

## 在ListView中 让图片自动适配屏幕

只要调整图片的宽度就好了。 只要宽度是100%，高度就会自动按照比例拉伸。

