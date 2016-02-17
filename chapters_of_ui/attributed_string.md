#AttributedString

用来单独的为某个段落中的部分文字增加样式。

比如“热烈欢迎”，这里面的“热烈”两个字可以与“欢迎”
两个字有不同的字体，以及字体大小，颜色等等属性。

## 例子

### 创建一个AttributedString数组，并显示在Label上。

```javascript
var win = Titanium.UI.createWindow({
  backgroundColor: '#ddd',
});

win.open();

var text = 'Titanium 看起来还是很有前景的！';

var attr = Titanium.UI.createAttributedString({
  text: text,
  attributes: [
    {
      type: Titanium.UI.ATTRIBUTE_BACKGROUND_COLOR,
      value: "red",
      range: [text.indexOf('看起来'), ('看起来').length]
    },
    {
      type: Titanium.UI.ATTRIBUTE_BACKGROUND_COLOR,
      value: "blue",
      range: [text.indexOf('还是'), ('还是').length]
    },
    {
    type: Titanium.UI.ATTRIBUTE_BACKGROUND_COLOR,
      value: "yellow",
      range: [text.indexOf('很有前景'), ('很有前景').length]
    }
  ]
});

var label = Titanium.UI.createLabel({
  left: 20,
  right: 20,
  height: Titanium.UI.SIZE,
  attributedString: attr
});

win.add(label);
```

效果如图所示：

![attributed_string](/images/ui_attributed_string.png)

### 依次添加属性（带下划线）

```javascript
var win = Titanium.UI.createWindow({
  backgroundColor: '#ddd',
});

win.open();

var text = 'Titanium 看起来还是很有前景的！';

var attr = Titanium.UI.createAttributedString({
  text: text
});

// 带有下划线的文本
attr.addAttribute({
  type: Titanium.UI.ATTRIBUTE_UNDERLINES_STYLE,
  value:Ti.UI.ATTRIBUTE_UNDERLINE_STYLE_SINGLE,
  range: [0, text.length]
});

var label = Titanium.UI.createLabel({
  left: 20,
  right: 20,
  height: Titanium.UI.SIZE,
  attributedString: attr
});

win.add(label);
```

效果如图所示：

![attributed_string_underscore](/images/ui_attributed_string_underscore.png)

### 注意

上面这个例子中，官网给的例子中在使用`addAttribute()`方法的时候，
只给定了type却没有给定value，这样是不会出现下划线的效果的。

根据它自己的文档是说：如果设定type为`Titanium.UI.ATTRIBUTE_UNDERLINES_STYLE`
或者` Titanium.UI.ATTRIBUTE_STRIKETHROUGH_STYLE`，
就必须使用它提供的对应的一些value的选项，
如`Titanium.UI.ATTRIBUTE_UNDERLINE_STYLE_NONE`,
`Titanium.UI.ATTRIBUTE_UNDERLINE_STYLE_SINGLE`等。
