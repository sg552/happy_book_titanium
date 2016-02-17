# TabGroup

TabGroup 是非常重要的视图布局，几乎所有app开发的布局都会用到它。

TabGroup由多个Tab组成。 每个Tab中包含一个Window.

TabGroup 跟Windows 一样，是顶级View.

![android](/images/ui_tabgroup_android.png) | ![ios](/images/ui_tabgroup_ios.png)
:---:|:---:
Android | iOS

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

## 注意

Android 上的TabGroups默认在上方，iOS的在下方。这一点要注意。

所以我们一般在Android上，不用TabGroup, 就直接点击图标，切换Window就好了。

刘明星解决了这个问题，可以把安卓的TabGroup组件放到下方。不过我认为以目前的
安卓机来看，性能不够流畅。所以大家可以凭情况来选用。

TODO 明星，你的解决方案。
