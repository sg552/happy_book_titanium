##Ti.UI.iPhone
本节介绍Titanium对于iPhone提供的一些优化和特殊的组件。

注：此章节的内容只对iPhone有用。

Titanium提供了某些iPhone打开窗口的动画效果，需要在window.open()方法中添加相应参数。

```javascript
window_name.open({modal:true,modalTransitionStyle:style,modalStyle:presentation,navBarHidden:true});
```
上面打开窗口的动画效果中，主要有`modalTransitionStyle`和`modalStyle`两个参数，分别是modalwindow的过度效果和modal window的显示样式。

modalTransitionStyle:
* MODAL_TRANSITION_STYLE_COVER_VERTICAL
* MODAL_TRANSITION_STYLE_CROSS_DISSOLVE
* MODAL_TRANSITION_STYLE_FLIP_HORIZONTAL
* MODAL_TRANSITION_STYLE_PARTIAL_CURL

modalStyle:
* MODAL_PRESENTATION_CURRENT_CONTEXT
* MODAL_PRESENTATION_FORMSHEET
* MODAL_PRESENTATION_FULLSCREEN
* MODAL_PRESENTATION_PAGESHEET

以下为从Titanium官方推出的展示所有组件效果的app(KitchenSink)中关于上面特效的一个效果展示图。

![cover vertial fullscreen](http://image.happysoft.cc/image/33/cover_vertical_Fullscreen.gif)
![flip horizontal fullscreen](http://image.happysoft.cc/image/39/flip_horizontal_fullscreen.gif)
![cross dissolve fullscreen](http://image.happysoft.cc/image/41/cross_dissolve_fullscreen.gif)
![partial curl fullscreen](http://image.happysoft.cc/image/42/partial_fullscreen.gif)

在Ti.UI.iPhone下还有许多子类，他们都是以Ti.UI.iPhone为命名空间。
* ActiveIndicatorStyle
* AlertDialogStyle
* AnimationStyle
* ListViewCellSelectionStyle
* ListViewScrollPosition
* ListViewSeparatorStyle
* ListViewStyle
* NavigationGroup
* ProgressBarStyle
* RowAnimationStyle
* ScrollIndicatorStyle
* StatusBar
* SystemButton
* SystemButtonStyle
* SystemIcon
* TableViewCellSelectionStyle
* TableViewScrollPosition
* TableViewSeparatorStyle
* TableViewStyle


###ActivityIndicatorStyle
iPhone样式的ActivityIndicator主要有三种样式:big、dark、plain,默认为plain。其中big和plain的颜色默认为白色，indicator在创建的时候默认为隐藏。动画效果见下图：
![activity indicator of iphone style](http://image.happysoft.cc/image/43/activity_indicator.gif)

###AlertDialogStyle
AlertDialog主要用于弹出对话框，在不同平台下的显示效果如下：
![Alert Dialog for all platform](http://image.happysoft.cc/image/48/alert_dialog.png)
针对iPhone有这几种样式：DEFAULT、LOGIN_AND_PASSWORD_INPUT、PLAIN_TEXT_INPUT、SECURE_TEXT_INPUT

* DEFAULT:默认的标准弹出对话框。
![default dialog](http://image.happysoft.cc/image/53/dialog_default.png)

* LOGIN_AND_PASSWORD_INPUT:弹出带有输入用户名和密码的对话框。
![login and password input](http://image.happysoft.cc/image/54/dialog_password.png)

* PLAIN_TEXT_INPUT:弹出一个带有输入框的对话框，用户可以自己输入内容。
![plain text input](http://image.happysoft.cc/image/55/dialog_plain.png)

* SECURE_TEXT_INPUT:弹出带有输入的对话框，输入内容会用黑点代替进行掩盖。
![secure text input](http://image.happysoft.cc/image/56/dialog_secure.png)
