# UI 的样式

大部分的UI 都继承于 Ti.UI.View. 可以说这个View 是Titanium UI的基础。

弄明白了它的样式，其他几乎所有的UI组件的样式就都明白了。

名称| 说明 | 例子 | 默认值
---|---|---|---
backgroundColor | 背景色 | 'red', "#334455" | Transparent
backgroundDisabledColor | 不可用时的背景色, 仅适用于android | 'red', "#334455" | Transparent
backgroundFocusedColor | 聚焦时的背景色, 仅用于android | 'red', "#334455" | Transparent
backgroundSelectedColor  | 被选中时的背景颜色, 仅用于android | 'red', "#334455" | Transparent
backgroundImage | 背景图片 | '/some/file.jpg', 'http://s.com/file.jpg' | 默认是没有图片的。但是对于一些特定的控制类的UI（button, text field )会使用系统自带的图片。
backgroundDisabledImage | 不可用时的背景图片, 仅用于android | '/some/file.jpg', 'http://s.com/file.jpg' | undefined , 但是如果 backgroundImage 有值的话就用它。
backgroundFocusedImage | 聚焦时的背景图片, 仅用于android | '/some/file.jpg', 'http://s.com/file.jpg' | undefined , 但是如果 backgroundImage 有值的话就用它。
backgroundSelectedImage | 被选中时的背景图片, 仅用于android | '/some/file.jpg', 'http://s.com/file.jpg' | undefined , 但是如果 backgroundImage 有值的话就用它。
backgroundRepeat | 背景图片是否重复, 对于ios上的button, label 和 textfield 是不支持的。  | true , false | false
borderColor  | 边框的颜色 | "red", "#334455" | 同 backgroundColor
borderRadius  | 边框的圆角度数。这个度数越大，说明边框的角越圆 | 0.2 | 0
borderWidth | 边框的宽度 | "10px" | 0
bubbleParent | 是否把事件继续冒泡到它的上级元素(parent) | true, false| true
layout | 布局 | 'composite', 'vertical', 'horizontal', 具体见 [布局](/chapters_of_senior/layouts_positioning_and_the_view_hierarchy.md) | composite
opacity | 透明度 | '0.5' | 1
height | 高度 | '10px', '50%' | Ti.UI.FILL 或 Ti.UI.SIZE
left | 到parent元素左边框的距离 | '10px', '50%'| 无默认值
right | 到parent元素右边框的距离 | '10px', '50%'| 无默认值
top | 到parent元素顶部边框的距离 | '10px', '50%'| 无默认值
bottom | 到parent元素底部边框的距离 | '10px', '50%'| 无默认值
width | 宽度, 可以是精确的数值，也可以如默认值中的常量。| "60px" | Ti.UI.FILL 或 Ti.UI.SIZE
zIndex | 显示时的优先级。跟CSS 一样，越高越排在前面。 | 10 | undefined
touchEnabled | 是否允许触摸事件 | true,false | true
visible | 是否可见 | true, false | true


其他的UI组件的属性查看方法也是一样的。
