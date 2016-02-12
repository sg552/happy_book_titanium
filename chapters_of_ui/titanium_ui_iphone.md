## iPhone独有的UI组件

本节介绍Titanium对于iPhone提供的一些优化和特殊的组件。

Titanium提供了某些iPhone打开窗口的动画效果，
需要在window.open()方法中添加相应参数。

```javascript
window_name.open({
  modal:true,
  modalTransitionStyle:style,
  modalStyle:presentation,
  navBarHidden:true
});
```
上面打开窗口的动画效果中，主要有`modalTransitionStyle`和`modalStyle`两个参数，
分别是modalwindow的过度效果和modal window的显示样式。

modalTransitionStyle:

- MODAL_TRANSITION_STYLE_COVER_VERTICAL
- MODAL_TRANSITION_STYLE_CROSS_DISSOLVE
- MODAL_TRANSITION_STYLE_FLIP_HORIZONTAL
- MODAL_TRANSITION_STYLE_PARTIAL_CURL

modalStyle:

- MODAL_PRESENTATION_CURRENT_CONTEXT
- MODAL_PRESENTATION_FORMSHEET
- MODAL_PRESENTATION_FULLSCREEN
- MODAL_PRESENTATION_PAGESHEET

以下为从Titanium官方推出的展示所有组件效果的app(KitchenSink)中关于上面特效的一个效果展示图。

1.从下方冒出来：

![cover vertial](/images/ui_iphone_cover_vertical.gif)

2.水平翻出来:

![flip horizontal](/images/ui_iphone_flip_horizontal.gif)

3.淡入淡出：

![cross dissolve](/images/ui_iphone_cross_dissolve.gif)

4.翻书页效果：

![partial curl](/images/ui_iphone_partial.gif)

在Ti.UI.iPhone下还有许多子类，他们都是以Ti.UI.iPhone为命名空间。

- ActiveIndicatorStyle
- AlertDialogStyle
- AnimationStyle
- ListViewCellSelectionStyle
- ListViewScrollPosition
- ListViewSeparatorStyle
- ListViewStyle
- NavigationGroup
- ProgressBarStyle
- RowAnimationStyle
- ScrollIndicatorStyle
- StatusBar
- SystemButton
- SystemButtonStyle
- SystemIcon
- TableViewCellSelectionStyle
- TableViewScrollPosition
- TableViewSeparatorStyle
- TableViewStyle
