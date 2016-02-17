##Titanium Alloy Views
###Alloy Views 简介
在Alloy中，View组件表示应用的UI，通常使用XML标记语言来写，对应的样式（Style）则采用Titanium的样式文件(.tss)来表示。类似于HTML和CSS的关系。

Alloy Views是对Titanium的SDK中UI对象的抽取，例如<View>标签可以表示Ti.UI.View对象的一个实例，使用Alloy框架的一个好处就是可以把视图层和逻辑控制层分开，使代码更加简洁可读性更高。View的视图文件被放在app/views/文件夹下，用xml文件表示。每一个对应的xml文件可以有与之对应的Controller文件(.js)或者Style文件(.tss)，编译时，xml文件会被编译成Titanium代码。
例如：使用Alloy框架时，默认生产的index.xml文件。
```xml
app/views/index.xml

<Alloy>
    <Window class="container">
        <Label id="label" onClick="doClick">Hello, World</Label>
    </Window>
</Alloy>

```
代码中在window里面放了一个label，id为“label”，并且添加了一个点击事件“doClick”，label上的文字为“Hello, World”。

Titanium中index通常做为App的入口。
