###ListViewCellSelectionStyle
ListViewCellSelectionStyle是ListView中selectionStyle的属性值常量，同时也是ListDataItem或者ItemTemplate中的属性的常量值，用来指定ListItem被选定的效果。
* BLUE: 选中背景颜色为蓝色
* GRAY: 选中背景颜色为灰色
* NONE: 选中背景颜色为空(没有选中颜色变化效果)

###ListViewScrollPosition
ListViewScrollPosition是ListViewAnimationProperties的属性值，当使用ListView的`scrollToItem`,`appendSection`,`deleteSectionAt`,`insertSectionAt`和`replaceSectionAt`等方法时会被触发。
* BOTTOM: ListView将感兴趣区滚动至ListView可见部分的底部
* MIDDLE: ListView将感兴趣区滚动至listview可见部分的中部
* TOP: ListView将感兴趣区滚动至listview可见部分的顶部
* NONE: ListView会移动最小的距离使感兴趣区最大的呈现在当前屏幕，如果这一行在可视范围外，会默认滚动到其顶部。NONE为默认设置。

###ListViewSeparatorStyle
ListViewSeparatorStyle是ListView中属性separatorStyle的属性值，用来指定ListView的每个Item间的分割线样式。主要有两种。
* NONE: 没有分割线
* SINGLE_LINE: 灰色的一条横线，为默认值。

###ListViewStyle
ListView的属性style的值。

* GROUPED: ListView的section之间表现出与一组row明显不同，section的header和footer不浮动。
* PLAIN: section的header和footer以插入行的形式作为行的分隔符，并当ListView滑动的时候会浮动。
