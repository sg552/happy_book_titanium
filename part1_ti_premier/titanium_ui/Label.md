#Label

**Label**是Titanium UI组件中最常用的一个**文本**显示UI组件，常被用来处理页面中**较短**或**中长型**的文本显示；非
必要情况下我们不建议使用Label来处理长文本和超长型的文本显示，对于长文本我们建议你使用**文本域**(Ti.UI.TextArea)
UI组件(详见**2.4.x**)。下面是一个Label的例子，你在Hello World项目中就已经接触过了：

```xml
    <Alloy>
        <Window class="container" id="my_window">
            <Label id="label" onClick="doClick">Hello,World</Label>
        </Window>
    </Alloy>
```

我们也可以在**.js**文件中动态创建Label：

```javascript
    var my_label = Ti.UI.createLabel({
        id:'label',
        width:'100%',
        height:'10%',
        text:'Hello,World'
    });

    my_label.addEventListener('click',doClick(e));   //label的点击事件，相当于.xml中的“onClick=doClick”
    $.my_window.add(my_label);                       //将创建的label添加到Window页面中
```

##1.Label常用的几个属性
(以下属性按首字母排序，不分先后)
###1.1 autoLink
**autoLink**将label中的指定类型的string转化成可点击的链接。Titanium提供了5种指定类型的string，分别为：

    ① Titanium.UI.AUTOLINK_CALENDAR：有问题，待解决
    ② Titanium.UI.AUTOLINK_EMAIL_ADDRESSES：将eamil类型的string转化成可点击的链接，点击后跳转到手机邮箱（仅支持Android）
    ③ Titanium.UI.AUTOLINK_MAP_ADDRESSES：将地址类型的string转化成可点击的链接，点击后将通过Google Map打开该地址。（仅支持Android。PS：目前Titanium的Map不支持中国地区的地理搜索，即该属性在中国地区内无法发送地理位置搜索请求。）
    ④ Titanium.UI.AUTOLINK_PHONE_NUMBERS：将电话号码类型的string转化成可点击的链接，点击后跳转到手机拨号页面。（仅支持Android）
    ⑤ Titanium.UI.AUTOLINK_URLS：将url类型的string转化成可点击的链接，点击后打开该url。（仅支持Android）

除了上述5种指定类型的string，Titanium还提供了以上全部类型检测的一个属性**Titanium.UI.AUTOLINK_ALL**。
该属性将自动检测string中所有可转化的类型，例如：

![imageview](http://image.happysoft.cc)

```xml
    <Label id='test_label' text='电话：18888888888\n 邮箱：test_eamil@qq.com\n 博客地址：http://www.mybolg.com'/>
```

```tss
   "#test_label":{
      width:'100%',
      autoLink:Titanium.UI.AUTOLINK_ALL
   }
```

###1.2 ellipsize
**ellipsize**属性待完成

###1.3 shadow
**shadow**是实现Label的string阴影效果的一种属性。Titanium提供3个预值来实现这种效果：

    ① shadowColor：描述string阴影的颜色。
    ② shadowOffset：描述string阴影相对于本体的偏移距离。
    ③ shadowRadius：描述string阴影的圆角值，使阴影字体更加圆滑。

**shadowOffset**有两个值**x**(水平方向上的偏移距离)，**y**(垂直方向上的偏移距离)。效果图如下：

![imageview](http://image.happysoft.cc)

###1.4 textAlign
**textAlign**描述Label字符串相对于Label边界的**水平对齐准线位**对齐。textAlign一共有3个预值，分别对应Label的“**左对齐准线位**”、
“**右对齐准线位**”以及“**居中准线位**”。

    ① Titanium.UI.TEXT_ALIGNMENT_LEFT：左对齐，字符串相对于Label边界向左靠拢。
    ② Titanium.UI.TEXT_ALIGNMENT_RIGHT：右对齐，字符串向相对于Label边界向右靠拢。
    ③ Titanium.UI.TEXT_ALIGNMENT_CENTER：水平居中对齐，字符串相对于Label边界水平居中靠拢。

如下所示效果：

![imageview](http://image.happysoft.cc)  ![imageview](http://image.happysoft.cc)  ![imageview](http://image.happysoft.cc)

相对应的，和textAlign相对于Label边界水平对齐的对齐效果属性是**verticalAlign**，处理字符串在**垂直方向**上相对于Label边界的对齐位；
它也有3个预值，如下：

    ① Titanium.UI.TEXT_VERTICAL_ALIGNMENT_TOP：顶部对齐，字符串相对于Label边界向顶部靠拢。
    ① Titanium.UI.TEXT_VERTICAL_ALIGNMENT_BOTTOM：底部对齐，字符串相对于Label边界向底部靠拢。
    ① Titanium.UI.TEXT_VERTICAL_ALIGNMENT_CENTER：垂直居中对齐，字符串相对于Label边界垂直居中靠拢。

![imageview](http://image.happysoft.cc)  ![imageview](http://image.happysoft.cc)  ![imageview](http://image.happysoft.cc)

Label默认情况下字符串水平、垂直居中。

###1.5 wordWrap
**wordWrap**属性设置Label中string的word

##2.Label常用的几个方法
