# Titanium.UI.iPad.Popover

一个iPad上面UI,展示一个暂时的消息。`<Popover></Popover>`标签可以作为最顶级的`View`。

示例图片:

![popover](http://image.happysoft.cc/image/40/titanium_ui_ipad_popover.gif)

在controller中创建一个popover:

```javascript
var win = Ti.UI.createWindow({backgroundColor: 'white'});

var button = Ti.UI.createButton({title: 'Open Popover!'});
button.addEventListener('click', function(e){
    popover.show({ view: button });
})
win.add(button);

var rightButton = Ti.UI.createButton({title: 'Robin'});
rightButton.addEventListener('click', function(e){
    alert("But green's the color of spring.");
});

var contentWindow = Ti.UI.createWindow({
    backgroundColor: 'green',
    rightNavButton: rightButton,
    title: 'Kermit',
    width: 250,
    height: 100
});
contentWindow.add(Ti.UI.createLabel({text: "It's not easy being green."}));

var popover = Ti.UI.iPad.createPopover({
    width: 250,
    height: 100,
    contentView: Ti.UI.iOS.createNavigationWindow({window: contentWindow})
});

win.open();
```

在view中使用popover:

```xml
<Alloy>
    <Popover height='100' width='250'>
        <ContentView>
            <NavigationWindow>
                <Window title='Kermit' backgroundColor='green'>
                    <RightNavButton onClick="showAlert" title="Robin" />
                    <Label>It's not easy being green.</Label>
                </Window>
            </NavigationWindow>
        </ContentView>
    </Popover>
</Alloy>
```
