#AttributedString
AttributedString 用于管理一个字符串，以及与该字符串中的单个字符或某些范围的字符串相关的属性。比如“热烈欢迎”，这里面的“热烈”两个字可以与“欢迎”两个字有不同的字体，以及字体大小，颜色等等属性。这就是AttributedString的作用。

##使用方法
使用`Titanium.UI.createAttributedString`方法。这其中文本的属性必须在创建这个AttributedString时候进行初始化。各种属性可以在构建方法中创建，也可以在之后创建。

##使用例子
###创建一个AttributedString数组，并显示在Label上。
```javascript
var win = Titanium.UI.createWindow({
  backgroundColor: '#ddd',
});

win.open();


var text =  'Bacon ipsum dolor Appcelerator Titanium rocks! sit amet fatback leberkas salami sausage tongue strip steak.';

var attr = Titanium.UI.createAttributedString({
    text: text,
    attributes: [
      // Underlines text
        {
        type: Titanium.UI.ATTRIBUTE_UNDERLINES_STYLE,
        range: [0, text.length]
        },
        // Sets a background color
        {
        type: Titanium.UI.ATTRIBUTE_BACKGROUND_COLOR,
        value: "red",
        range: [text.indexOf('Appcelerator'), ('Appcelerator').length]
        },
        {
        type: Titanium.UI.ATTRIBUTE_BACKGROUND_COLOR,
        value: "blue",
        range: [text.indexOf('Titanium'), ('Titanium').length]
        },
        {
        type: Titanium.UI.ATTRIBUTE_BACKGROUND_COLOR,
              value: "yellow",
              range: [text.indexOf('rocks!'), ('rocks!').length]
        },
          // Sets a foreground color
        {
        type: Titanium.UI.ATTRIBUTE_FOREGROUND_COLOR,
              value: "orange",
              range: [0,  text.length]
        },
        {
        type: Titanium.UI.ATTRIBUTE_FOREGROUND_COLOR,
              value: "black",
            range: [text.indexOf('rocks!'), ('rocks!').length]
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
![simple attributedstring](http://image.happysoft.cc/image/51/屏幕快照 2015-09-07 下午1.58.10.png)

###依次添加属性（带下划线）
```javascript
var win = Titanium.UI.createWindow({
  backgroundColor: '#ddd',
});

win.open();

var text =  'Bacon ipsum dolor Appcelerator Titanium rocks! sit amet fatback leberkas salami sausage tongue strip steak.';

var attr = Titanium.UI.createAttributedString({
  text: text
});

// Underlines text
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
![underline_string](http://image.happysoft.cc/image/52/屏幕快照 2015-09-07 下午2.50.59.png)

###注意
上面这个例子中，官网给的例子中在使用`addAttribute()`方法的时候，只给定了type却没有给定value，这样是不会出现下划线的效果的。

根据它自己的文档是说：如果设定type为` Titanium.UI.ATTRIBUTE_UNDERLINES_STYLE` 或者` Titanium.UI.ATTRIBUTE_STRIKETHROUGH_STYLE`，就必须使用它提供的对应的一些value的选项，如`Titanium.UI.ATTRIBUTE_UNDERLINE_STYLE_NONE`,`Titanium.UI.ATTRIBUTE_UNDERLINE_STYLE_SINGLE`等等。
