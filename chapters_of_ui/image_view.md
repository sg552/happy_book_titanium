# Titanium.UI.ImageView

## 介绍

一个展示图片或动态图片的组件,静态图片支持android里面的Nine-patch和Draw 9-patch图片文件。

### 基本的图片组件创建示例

![image](http://image.happysoft.cc/image/30/titanium_ui_imageview.png)

controller创建方式:

```javascript
Ti.UI.backgroundColor = 'white';
var win = Ti.UI.createWindow();
var image = Ti.UI.createImageView({
  //image:'/images/bdlogo.png'
  image:'https://www.baidu.com/img/bdlogo.png'
});
win.add(image);
win.open();
```

view创建方式:

```xml
<Alloy>
    <Window backgroundColor="white">
        <ImageView id="image" image="https://www.baidu.com/img/bdlogo.png" />
    </Window>
</Alloy>
```

* 需要提及的是`//image:'/images/bdlogo.png'`这行代码中的文件路径实际在项目中的位置是*app/assets/images/bdlogo.png*,在使用`image`属性的时候不需要加上*app/assets*路径。

* 在不指定宽高的情况下android上面的图片展示样式和ios有区别。

* 在android上面部分机型对图片的宽高有最大值限制。

### nine_patch的图片组件创建示例:

![imageview](http://image.happysoft.cc/image/37/imageview_9_pach.gif)

图片文件:[custom-slider-right.9.png](https://github.com/appcelerator/titanium_mobile/raw/master/demos/KitchenSink/Resources/images/custom-slider-right.9.png) [custom-slider-left.9.png](https://github.com/appcelerator/titanium_mobile/raw/master/demos/KitchenSink/Resources/images/custom-slider-right.9.png)

> liunx 或 mac 的同学可以用`wget＋url`的方式download图片到app/assets/images目录下面

```javascript
var win = Ti.UI.createWindow({
    backgroundColor: 'white',
    exitOnClose: true,
    fullscreen: false,
    title: 'Click button to test',
    layout: 'vertical'
});

var button = Ti.UI.createButton({
    backgroundImage: '/images/custom-slider-right.9.png',
    backgroundSelectedImage:'/images/custom-slider-left.9.png',
    title: 'Click me!',
    top: 50, 
    width: 100,
    height: 50
});
var button2 = Ti.UI.createButton({
    backgroundImage: '/images/custom-slider-right.9.png',
    backgroundSelectedImage:'/images/custom-slider-left.9.png',
    title: 'Click me!',
    top: 50, 
    width: 300,
    height: 500 
});
button.addEventListener('click',function(e){
    Ti.API.info("You clicked the button");
});
win.add(button);
win.add(button2);
win.open();
```
