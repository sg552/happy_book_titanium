# Titanium.UI.ButtonBar(Only IOS)

> 以下代码参考与KitchenSink
 
![ButtonBar](http://image.happysoft.cc/image/9/ti_ui_buttonbar.png)

controller创建方式:

```javascript
var buttonbar = Titanium.UI.createButtonBar({
    labels:['One', 'Two', 'Three'],
    backgroundColor:'#777',
    top:50,
    style:Titanium.UI.iPhone.SystemButtonStyle.BAR,
    height:25,
    width:200
});
win.add(buttonbar);
```

view创建方式:

```xml
<Alloy>
    <Window id="win">
        <ButtonBar id="buttonbar" platform="ios" backgroundColor="#777" top="50" height="25" width="200">
            <!-- 可以通过 ButtonBar.labels 设置 -->
            <Labels>
                <!-- Specify text with node text or the title attribute. -->
                <!-- Can also specify the enabled, image and width attributes. -->
                <Label>One</Label>
                <Label>Two</Label>
                <Label>Three</Label>
            </Labels>
            <!-- Place additional views for the ButtonBar here. -->
        </ButtonBar>
    </Window>
</Alloy>
```

* xml里面的的 `platform = "ios"`定义`<ButtonBar></ButtonBar>`里面的代码只当在ios平台的时候会生效。