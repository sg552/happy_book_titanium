# Creating an Attributed String (创建一个字符串属性)
如果你使用attributedstring或attributedhinttext属性，不设置任何其他属性，修改文字的外观，如字体，颜色，等等，如果你使用一个属性字符串，只使用一个属性的字符串。
Ti不支持使用属性字符串与其他文本修改属性。

例子app.js:

```javascript

var win = Ti.UI.createWindow({
     backgroundColor: '#ddd',
});
var text = "Have you tried hyperloop yet?";
var attr = Ti.UI.createAttributedString({
     text: text,
     attributes: [{
          type: Ti.UI.ATTRIBUTE_BACKGROUND_COLOR,
          value: "yellow",
          range: [text.indexOf('hyperloop'), ('hyperloop').length]
          }]
});
var label = Ti.UI.createLabel({
          attributedString: attr
});

win.add(label);
win.open();
```

设置类型属性titanium.ui.attribute_font和自定义字体字典价值属性来描述字体属性。

![](http://docs.appcelerator.com/platform/latest/images/download/attachments/37538231/Font.png)


```javascript
var text = "Have you tried hyperloop yet?";
var attr = Ti.UI.createAttributedString({
        text: text,
        attributes: [{
            type: Ti.UI.ATTRIBUTE_FONT,
            value: { fontSize: 24, fontFamily: 'Didot' },
            range: [text.indexOf('hyperloop'), ('hyperloop').length]
           }]
});
```


![](http://docs.appcelerator.com/platform/latest/images/download/attachments/37538231/ForegroundColor.png)

```javascript
var text = "Have you tried hyperloop yet?";
var attr = Ti.UI.createAttributedString({
      text: text,
      attributes: [{
            type: Ti.UI.ATTRIBUTE_FOREGROUND_COLOR,
            value: 'cyan',
            range: [text.indexOf('hyperloop'), ('hyperloop').length]
       }]
});

```

![](http://docs.appcelerator.com/platform/latest/images/download/attachments/37538231/BackgroundColor.png)

```javascript
var text = "Have you tried hyperloop yet?";
var attr = Ti.UI.createAttributedString({
      text: text,
      attributes: [{
          type: Ti.UI.ATTRIBUTE_BACKGROUND_COLOR,
          value: "yellow",
          range: [text.indexOf('hyperloop'), ('hyperloop').length]
      }]
});
```

![](http://docs.appcelerator.com/platform/latest/images/download/attachments/37538231/Underline.png)


```javascript
var text = "Have you tried hyperloop yet?";
var attr = Ti.UI.createAttributedString({
        text: text,
        attributes: [{
            type: Ti.UI.ATTRIBUTE_UNDERLINES_STYLE,
            value: Ti.UI.ATTRIBUTE_UNDERLINE_STYLE_DOUBLE | Ti.UI.ATTRIBUTE_UNDERLINE_PATTERN_DOT, // Ignored by Android only displays a single line
            range: [text.indexOf('hyperloop'), ('hyperloop').length]
        }]
});
```

![](http://docs.appcelerator.com/platform/latest/images/download/attachments/37538231/Strikethrough.png)


```javascript
var text = "Have you tried hyperloop ti.next yet?";
var attr = Ti.UI.createAttributedString({
       text: text,
       attributes: [{
           type: Ti.UI.ATTRIBUTE_STRIKETHROUGH_STYLE,
           value: Ti.UI.ATTRIBUTE_UNDERLINE_STYLE_THICK, // Ignored by Android only displays a single line
           range: [text.indexOf('hyperloop'), ('hyperloop').length]
       }]
});

```

![](http://docs.appcelerator.com/platform/latest/images/download/attachments/37538231/Link.png)


```javascript
var win = Ti.UI.createWindow({
     backgroundColor: '#ddd',
});
var text = "Have your tried hyperloop yet?";
var attr = Ti.UI.createAttributedString({
     text: text,
     attributes: [{
          type: Titanium.UI.ATTRIBUTE_LINK,
          value: "https://github.com/appcelerator/hyperloop",
          range: [text.indexOf('hyperloop'), ('hyperloop').length]
      }]
});

var label = Ti.UI.createLabel({
      attributedString: attr
});

label.addEventListener('link', function(e){
      Ti.API.info(JSON.stringify(e));
});

win.add(label);
win.open();
```

###iOS的属性,以下属性仅适用于iOS平台。

![](http://docs.appcelerator.com/platform/latest/images/download/attachments/37538231/Ligatures.png)

```javascript
var text = "fee-fi-fo-fum\nfee-fi-fo-fum";
var attr = Ti.UI.createAttributedString({
       text: text,
       attributes: [{
          type: Ti.UI.ATTRIBUTE_FONT,
          value: { fontSize: 24, fontFamily: Cochin-Italic' },
          range: [0, text.length]},
          {
          type: Titanium.UI.ATTRIBUTE_LIGATURE,
          value: 0,
          range: [4, 1]
           }]
});

```

字距调整
字距调整字符间距。指定你的字符串的一部分不同的字距，设置类型属性titanium.ui.attribute_kern和浮点值点指定字符之间的距离值属性。将值设置为0进制的调整，这是默认行为。


![](http://docs.appcelerator.com/platform/latest/images/download/attachments/37538231/Kerning.png)


```javascript
var text = "Have you tried hyperloop yet?";
var attr = Ti.UI.createAttributedString({
      text: text,
      attributes: [{
          type: Ti.UI.ATTRIBUTE_KERN,
          value: 5.0,
          range: [text.indexOf('hyperloop'), ('hyperloop').length]
      }]
 });
```
使用你的行程文本字符串的一部分，在属性字典，设置类型属性titanium.ui.attribute_stroke_width和浮子描述轮廓尺寸的价值属性。正面的值只显示字符的轮廓，而负值填充字符。
改变文字的颜色，设置类型属性titanium.ui.attribute_stroke_color和颜色名称或十六进制值属性。


![](http://docs.appcelerator.com/platform/latest/images/download/attachments/37538231/Outline.png)


```javascript
var text = "Have you tried hyperloop yet?";
var attr = Ti.UI.createAttributedString({
      text: text,
      attributes: [{
          type: Ti.UI.ATTRIBUTE_STROKE_COLOR,
          value: 'red',
          range: [text.indexOf('hyperloop'), ('hyperloop').length]
      },
     {
      type: Ti.UI.ATTRIBUTE_STROKE_WIDTH,
      value: 3.0,
      range: [text.indexOf('hyperloop'), ('hyperloop').length]
     }]
});

```

![](http://docs.appcelerator.com/platform/latest/images/download/attachments/37538231/Shadow.png)

```javascript
var text = "Have you tried hyperloop yet?";
var attr = Ti.UI.createAttributedString({
        text: text,
        attributes: [{
             type: Ti.UI.ATTRIBUTE_SHADOW,
             value: {color: 'green', offset: {width: 10, height: 5}},
             range: [0, text.length]
        }]
});
```

![](http://docs.appcelerator.com/platform/latest/images/download/attachments/37538231/Letterpress.png)

```javascript
var text = "Have you tried hyperloop yet?";
var attr = Ti.UI.createAttributedString({
      text: text,
      attributes: [{
           type: Ti.UI.ATTRIBUTE_TEXT_EFFECT,
           value: Ti.UI.ATTRIBUTE_LETTERPRESS_STYLE,
           range: [text.indexOf('hyperloop'), ('hyperloop').length]}
});

```

![](http://docs.appcelerator.com/platform/latest/images/download/attachments/37538231/Baseline.png)

```javascript
var text = "Have your tried hyperloop yet?";
var attr = Ti.UI.createAttributedString({
      text: text,
      attributes: [{
          type: Ti.UI.ATTRIBUTE_BASELINE_OFFSET,
          value: 10,
          range: [text.indexOf('hyperloop'), ('hyperloop').length]
      }]
});
```

![](http://docs.appcelerator.com/platform/latest/images/download/attachments/37538231/Oblique.png)

```javascript
var text = "Have your tried hyperloop yet?";
var attr = Ti.UI.createAttributedString({
     text: text,
     attributes: [{
         type: Ti.UI.ATTRIBUTE_OBLIQUENESS,
         value: 0.25,
         range: [text.indexOf('hyperloop'), ('hyperloop').length]
     }]
});

```

![](http://docs.appcelerator.com/platform/latest/images/download/attachments/37538231/Expansion.png)

```javascript
var text = "Have your tried hyperloop yet?";
var attr = Ti.UI.createAttributedString({
      text: text,
      attributes: [{
          type: Titanium.UI.ATTRIBUTE_EXPANSION,
          value: 0.25,
          range: [text.indexOf('hyperloop'), ('hyperloop').length]
     }]
});
```
