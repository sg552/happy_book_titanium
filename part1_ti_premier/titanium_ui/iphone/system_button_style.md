###SystemButtonStyle
Button中style属性的属性值。设定系统图标的样式，作用于`Button`,`ButtonBar`和`TabbedBar`这些UI组件。
不同的类型用在不同的地方，使用下面样式时一般的按钮不能放在navbar,toolbar或者tabbed bar中:
* BORDERED: 简单的按钮样式带有圆角的边框，背景为白色。普通按钮的默认样式
* DONE: 样式与bordered样式相似，背景为蓝色，Button的样式表示完成，如：`OK`,`Sava`,`Go`等
* PLAIN: 最原始的按钮，没有任何修饰

注：如果使用`PLAIN`样式，就必须给按钮指定其他的属性。例如：如果设置`backgroundSelectedImage`和`selectedColor`就没有按钮按下后的效果。

如果将Button加入到ToolBar中，这些样式会有一些其他的效果：
* PLAIN样式会对没有修饰的Button设置为大的字号，按下时带有阴影效果。为默认的样式。
* BORDERED 带有圆角的边框，背景为浅蓝色的简单按钮
* DONE 和BORDERED样式类似，背景为深蓝色

对于`TabbedBar`和`ButtonBar`,三种样式有以下的意义：
* PLAIN ButtonBar和TabbedBar的默认的样式
* BORDERED 类似于PLAIN样式，但边框较宽
* BAR 在ButtonBar和TabbedBar中显示的更加紧凑，半透明，可以呈现一些背景的颜色
