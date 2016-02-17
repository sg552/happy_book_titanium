# TableView 的样式

## TableViewCellSelectionStyle

设定`TableViewRow`被选定时的样式。为selectionStyle的属性值常量。

- BLUE: 被选中单元背景色变为蓝色。默认值
- GRAY: 被选中单元背景色为灰色
- NONE: 单元选中不变色，没有被选中效果

## TableViewScrollPosition

位置属性常量，作为TableView的位置属性值，使用`scrollToIndex`时触发

- BOTTOM: 将感兴趣区滚动到TableView可视区域底部
- MIDDLE: 将感兴趣区滚动到TableView可视区域中部
- NONE: 滚动最小的区域使感兴趣区能够完全被显示出来，如果已经全部可见则不滚动。
如果在可视区域以外，则触发`TOP`属性。
- TOP: 将感兴趣区滚动到TableView可视区域顶部

## TableViewSeparatorStyle

TableView的属性`separatorStyle`的属性值常量

- NONE: 没有明显的分界
- SINGLE_LINE: 使用一条与TableView等宽的直线作为分界线，默认值

##TableViewStyle

TableView的属性`style`的属性值

- GROUPED: TableView的section与一组row明显不同，section的header和footer不浮动
- PLAIN: 没有修饰的TableView，section的header和footer以inline的方式作为分隔标记，
并且在滚动的时候会浮动。
