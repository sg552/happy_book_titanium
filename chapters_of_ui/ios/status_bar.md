# StatusBar

状态栏样式和动画效果。

动画：状态栏动画效果可以用在`Titanium.UI.iPhone.showStatusBar`和
`Titanium.UI.iPhone.hideStatusBar`方法中,动画效果有:

- ANIMATION_STYLE_FADE: 当状态栏显示或隐藏时，以淡化效果展示。
- ANIMATION_STYLE_NONE: 显示或隐藏状态栏时，没有动画效果
- ANIMATION_STYLE_SLIDE: 显示或隐藏状态栏时，以滑动的方式展示

样式：状态栏的样式。用于`Titanium.UI.iPhone.statusBarStyle`和
`Titanium.UI.Window.statusBarStyle`属性，样式常量有：

- DEFAULT: 默认样式
- GRAY: 灰色状态栏
- GREY：灰色状态栏，同GARY
- LIGHT_CONTENT: 适用于暗色背景，在IOS7及以上有效,在IOS7以下版本使用，会以`TRANSLUCENT_BLACK`代替
- OPAQUE_BLACK: 不透明黑色状态栏,在IOS7及以上版本已被弃用，使用`LIGHT_CONTENT`代替
- NSLUCENT_BLACK: 透明黑色状态栏，在IOS7及以上有效,在IOS7以下版本使用，会以`TRANSLUCENT_BLACK`代替
