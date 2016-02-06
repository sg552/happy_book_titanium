#NavigationWindow
NavigationWindow是专门用于iOS中的层级内容导航管理的东西。

##创建方法
你可以使用`Titanium.UI.iOS.createNavigationWindow`方法，也可以在Alloy框架中使用`<NavigationWindow>`标签对来创建一个NavigationWindow。

所有的NavigationWindow对象都至少要有一个根window，并且不能删除它。当创建完一个NavigationWindow对象的时候，要通过`window`属性来设置它的根window。同样的，在Alloy中需要在`<NavigationWindow>`标签对中，添加一个`<Window></Window>`的标签对。

##例子
创建一个navigation group，第一个window是红色，按下按钮打开蓝色的window。通过返回键回到红色的根window。

```javascript
var win2 = Titanium.UI.createWindow({
    backgroundColor: 'red',
    title: 'Red Window'
});

var win1 = Titanium.UI.iOS.createNavigationWindow({
   window: win2
});

var win3 = Titanium.UI.createWindow({
    backgroundColor: 'blue',
    title: 'Blue Window'
});

var button = Titanium.UI.createButton({
    title: 'Open Blue Window'
});
button.addEventListener('click', function(){
    win1.openWindow(win3, {animated:true});
});

win2.add(button);
var button2 = Titanium.UI.createButton({
    title: 'Close Blue Window'
});
button2.addEventListener('click', function(){
    win1.closeWindow(win3, {animated:false}); //win3.close() will also work!!
});

win3.add(button2);
win1.open();
```

在Alloy中实现上面的效果：

app/views/index.xml
```xml
<Alloy>
    <NavigationWindow id="win1" platform="ios">
        <Window id="win2" title="Red Window" backgroundColor="red">
            <Button id="button" onClick="openBlueWindow">Open Blue Window</Button>
        </Window>
    </NavigationWindow>
</Alloy>
```

app/controllers/index.js
```javascript
function openBlueWindow(e) {
    var win3 = Alloy.createController('bluewin').getView();
    $.win1.openWindow(win3);
}

$.win1.open();
```

app/view/bluewin.xml
```xml
<Alloy>
    <Window id="win3" title="Blue Window" backgroundColor="blue">
        <Button onClick="closeWindow">Close Window</Button>
    </Window>
</Alloy>
```

app/controllers/bluewin.js
```javascript
function closeWindow(){
    $.win3.close();
}
```
