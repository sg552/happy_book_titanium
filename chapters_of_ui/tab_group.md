# TabGroup

TabGroup 是非常重要的视图布局，几乎所有app开发的布局都会用到它。

TabGroup由多个Tab组成。 每个Tab中包含一个Window.

TabGroup 跟Windows 一样，是顶级View.

![tab group](/images/ui_tab_group.png)

```js

Titanium.UI.setBackgroundColor('#000');

var tabGroup = Titanium.UI.createTabGroup();
var win1 = Titanium.UI.createWindow({
    title:'Tab 1',
    backgroundColor:'#fff'
});
var tab1 = Titanium.UI.createTab({
    icon:'KS_nav_views.png',
    title:'Tab 1',
    window:win1
});
var label1 = Titanium.UI.createLabel({
	color:'#999',
	text:'I am Window 1',
	font:{fontSize:20,fontFamily:'Helvetica Neue'},
	textAlign:'center',
	width:'auto'
});

win1.add(label1);


var win2 = Titanium.UI.createWindow({
    title:'Tab 2',
    backgroundColor:'#fff'
});
var tab2 = Titanium.UI.createTab({
    icon:'KS_nav_ui.png',
    title:'Tab 2',
    window:win2
});
var label2 = Titanium.UI.createLabel({
	color:'#999',
	text:'I am Window 2',
	font:{fontSize:20,fontFamily:'Helvetica Neue'},
	textAlign:'center',
	width:'auto'
});

win2.add(label2);

tabGroup.addTab(tab1);
tabGroup.addTab(tab2);

tabGroup.open();
```

