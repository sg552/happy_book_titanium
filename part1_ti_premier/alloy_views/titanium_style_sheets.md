###Titanium 样式(TSS)
前面章节介绍了怎么使用Alloy框架搭建UI，通常我们把布局和属性设置直接写入视图文件即可，但Titanium为了使代码可读性更高提高代码的重用性，提供了把属性值单独分开的方法--Titanium Style Sheets(TSS)。所有能够写在XML中的属性都可以写在TSS中。

TSS中有三种类型的字段：标签元素、class值、id值。其中class值需要在前面加`'.'`，id值需要在前面加`'#'`。在TSS中只允许存在以下类型的值：
* JSON值：字符串，数字，对象数组，布尔类型，null
* Titanium SDK 常量。例如：`Ti.UI.SIZE`
* Localization function(本地化方法)，例如Ti.Locale.getString()
* 命名空间为Alloy.CFG或者Alloy.Globals的变量
* 位运算符(>>,<<,>>>,&,|,^)

```css
".wrapper_view":{
    backgroundColor: gray;
}

"#blue_label":{
    backgroundColor: blue;
    borderRadius: 8;
}

"ImageView":{
    defaultImage: logo.png;
}
```

Titanium定义了一个全局化的初始化样式`app/style/app.tss`文件，在app.tss中定义的样式会成为app的默认设置，并且这些初始值可以在对应的tss文件和xml文件中被重写。

>属性优先级:id类型 > class类型 > 元素标签类型

在TSS中可以使用`platform`,`formFactor`属性进行平台判定和设备尺寸判定以确定对不同平台不同设备做相应的处理。可以使用`'!'`表示非，多个值之间用`','`隔开。

```css
"Button[platform=ios formFactor=handheld]":{
    backgroundColor: blue;
    title: iPhone;
}
"Button[platform=android formFactor=handheld]":{
    backgroundColor: red;
    title: android phone;
}
"Button[platform=ios,android  formFactor=tablet]":{
    backgroundColor: yellow;
    title: iPad or android pad;
}
"Button[platform=!ios]":{
    backgroundColor: gray;
    title: not ios;
}
```
####自定义样式属性
自动以的属性需要返回一个bool类型的值，自定义类型可以通过Alloy.createController()方法来传递，然后在XML和TSS中都能通过`'$.args.xxxx'`访问。

```javascript
app/controllers/index.js

function blueButton(e) {
    Alloy.createController('different_button' , {open_blue: true}).getView().open();
}

function redButton(e) {
    Alloy.createController('different_button' , {open_red: true}).getView().open();
}
```
```css
app/styles/different_button.tss

"Button[if=$.args.open_blue]":{
    backgroundColor: blue;
    title: blue;
}
"Button[if=$.args.open_red]":{
    backgroundColor: red;
    title: red;
}
```
```xml
app/views/different_button.xml

<Alloy>
    <Window>
        <Button if='$.args.open_blue' backgroundColor='blue' title='blue'/>
        <Button if='$.args.open_red' backgroundColor='red' title='red'/>
    </Window>
</Alloy>
```
