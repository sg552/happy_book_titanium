# Titanium.UI.Button

> TODO：此处用的Titanium官方的图片和例子

![android](http://docs.appcelerator.com/platform/latest/images/button/button_android.png)  | ![ios](http://docs.appcelerator.com/platform/latest/images/button/button_ios.png) | ![mobileweb](http://docs.appcelerator.com/platform/latest/images/button/button_mobileweb.png)  | ![windows phone](http://docs.appcelerator.com/platform/latest/images/button/button_wp.png)
------------- | ------------- | ------------- | -------------
android  | ios | mobileweb | windows phone

在controller中创建Button的例子:

*app/controllers/button.js*

```javascript
var button = Titanium.UI.createButton({
   title: 'Hello',
   top: 10,
   width: 100,
   height: 50
});
button.addEventListener('click',function(e)
{
   Titanium.API.info("You clicked the button");
});
```
在View中创建Button的例子:

*app/views/button.xml*

```xml
<Alloy>
    <Window id="win" backgroundColor="white">
        <!-- The title property can also be defined as node text. -->
        <Button id="button" onClick="doClick" title="Hello" top="10" width="100" height="50" />
    </Window>
</Alloy>
```

*app/controllers/button.js*

```javascript
function doClick(e){
    Titanium.API.info("You clicked the button");
};
```
Button在UI布局中是一个重要的控件。

> 以下 WP 指Windows Phone

需要注意的是不同平台的区别及其特殊的地方:

* android 和 WP 有focus事件
* android 和 Mobile Web 有 `backgroundSelectedColor` 这些属性和对应的get和set方法
* ios 有两个特殊的属性, `style`和`systemButton`,针对不同的IOS版本,一些特殊的属性效果也不一致。一些`systemButton`也被应用在很多`UI`和系统功能上,如**Camera** button。

常用事件:

* `click`(点击事件)
* `dblclick`(双击事件)
* `longclick`(长按事件)
