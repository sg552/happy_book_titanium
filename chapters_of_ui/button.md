# Titanium.UI.Button

Button在UI布局中是一个重要的控件。

![android](/images/ui_button_android.png) | ![ios](/images/ui_button_ios.png) | ![wp](/images/button_wp.png)
:---:|:---:|:---:|:---:
android | ios | Windows phone

## 例子

```javascript
var button = Titanium.UI.createButton({
  title: 'Hello',
  top: 10,
  width: 100,
  height: 50
});

button.addEventListener('click',function(e)
{
  Titanium.API.info("你点击了button");
});
```

需要注意的是不同平台的区别及其特殊的地方:

- android 和 Windows phone 有focus事件
- android 和 Mobile Web 有 `backgroundSelectedColor` 这些属性和对应的get和set方法
- ios 有两个特殊的属性, `style`和`systemButton`,针对不同的IOS版本,一些特殊的属性效果也不一致。一些`systemButton`也被应用在很多`UI`和系统功能上,如**Camera** button。

常用事件:

- `click`(点击事件)
- `dblclick`(双击事件)
- `longclick`(长按事件)
