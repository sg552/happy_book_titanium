# Label

Label是最常用的组件，常被用来处理页面中较短或中长型的文本显示；
非必要情况下我们不建议使用Label来处理长文本和超长型的文本显示，
对于长文本我们建议你使用TextArea。

## 例子

```javascript
var window = Ti.UI.createWindow();
var hello = Ti.UI.createLabel({
    id:'label',
    width:'100%',
    height:'10%',
    text:'Hello,World'
});
window.add(hello);
```

## 常用的几个属性

### (仅限Android)自动把字符串转换成特定的链接

使用 autoLink 属性，可用的值分别为：

- Ti.UI.AUTOLINK_CALENDAR：转换成日历。仅支持IOS。
- Ti.UI.AUTOLINK_EMAIL_ADDRESSES：将eamil类型的string转化成可点击的链接，点击后跳转到手机邮箱（仅支持Android）
- Ti.UI.AUTOLINK_MAP_ADDRESSES：将地址类型的string转化成可点击的链接，点击后将通过Google Map打开该地址。（仅支持Android。PS：目前Titanium的Map不支持中国地区的地理搜索，即该属性在中国地区内无法发送地理位置搜索请求。）
- Ti.UI.AUTOLINK_PHONE_NUMBERS：将电话号码类型的string转化成可点击的链接，点击后跳转到手机拨号页面。（仅支持Android）
- Ti.UI.AUTOLINK_URLS：将url类型的string转化成可点击的链接，点击后打开该url。（仅支持Android）

除了上述5种指定类型的string，Titanium还提供了以上全部类型检测的一个属性
Titanium.UI.AUTOLINK_ALL。 该属性将自动检测string中所有可转化的类型，例如：

![autolink](/images/label_autolink.gif)

源代码如下：
```js
var win = Ti.UI.createWindow();
var label = Ti.UI.createLabel({
  text: '电话：18888888888\n' +
        '邮箱：test_eamil@qq.com\n' +
        '博客地址：http://www.mybolg.com',
  width: '100%',
  autoLink: Ti.UI.AUTOLINK_ALL
});
win.add(label);
win.open();
```

### 截短过长的文字

使用 ellipsize。

可用的值：

- Ti.UI.TEXT_ELLIPSIZE_TRUNCATE_START:  在行首截短。
- Ti.UI.TEXT_ELLIPSIZE_TRUNCATE_MIDDLE: 在行中截短。
- Ti.UI.TEXT_ELLIPSIZE_TRUNCATE_END: 在行末截短。
- Ti.UI.TEXT_ELLIPSIZE_TRUNCATE_MARQUEE: 表现同行末截短。

![ellipsize](/images/ui_label_ellipsize.png)

```js
var win = Ti.UI.createWindow();
win.backgroundColor = 'white';
var label = Ti.UI.createLabel({
  text: '我是好长好长好长好长好长好长好长好长' +
        '好长好长好长好长好长好长好长好长好长' +
        '好长好长好长好长好长好长好长好长好长' +
        '好长好长好长好长好长好长好长好长好长' +
        '好长好长好长好长好长好长好长的文字',
  width: '50%',
  height: '20',
  ellipsize: Ti.UI.TEXT_ELLIPSIZE_TRUNCATE_END
});
win.add(label);
win.open();
```

### 实现阴影效果

shadow是实现Label的string阴影效果的一种属性。

Titanium提供3个预值来实现这种效果：

- shadowColor：描述string阴影的颜色。
- shadowOffset：描述string阴影相对于本体的偏移距离。
- shadowRadius：描述string阴影的圆角值，使阴影字体更加圆滑。

shadowOffset有两个值:

- x(水平方向上的偏移距离)，
- y(垂直方向上的偏移距离)。

效果图如下：

![shadow](/images/label_shadow.png)

## 文字对齐

textAlign: 描述Label字符串相对于Label边界的水平对齐准线位对齐。

textAlign的可用值有：

- Ti.UI.TEXT_ALIGNMENT_LEFT：左对齐，字符串相对于Label边界向左靠拢。
- Ti.UI.TEXT_ALIGNMENT_RIGHT：右对齐，字符串向相对于Label边界向右靠拢。
- Ti.UI.TEXT_ALIGNMENT_CENTER：水平居中对齐，字符串相对于Label边界水平居中靠拢。

如下所示效果：

![imageview](/images/label_text_align.png)

相对应的，和textAlign相对于Label边界水平对齐的对齐效果属性是verticalAlign，
处理字符串在垂直方向上相对于Label边界的对齐位；

verticalAlign的可用值有：

- Ti.UI.TEXT_VERTICAL_ALIGNMENT_TOP：顶部对齐，字符串相对于Label边界向顶部靠拢。
- Ti.UI.TEXT_VERTICAL_ALIGNMENT_BOTTOM：底部对齐，字符串相对于Label边界向底部靠拢。
- Ti.UI.TEXT_VERTICAL_ALIGNMENT_CENTER：垂直居中对齐，字符串相对于Label边界垂直居中靠拢。

![imageview](/images/label_text_vertical_align.png)

Label默认情况下字符串水平、垂直居中。

