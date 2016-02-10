# DashboardView 和 DashboardItem

DashboardView和DashboardItem是IOS的特殊组件,
DashboardView包含多个DashboardItem而组成一个Dashboard。

DashboardView里面的东西会以3x3的样式在DashboardView中展现,
当超过9个的数量时,会以第二页的形式存储在一个scrollableView中。

![dashboard](/images/ui_ios_dashboard.gif)

## 例子

```javascript

var win = Ti.UI.createWindow({
    backgroundColor: '#13386c'
});

var button = Ti.UI.createButton({
    title: '编辑',
    style: Ti.UI.iPhone.SystemButtonStyle.DONE,
});

var toolbar = Ti.UI.iOS.createToolbar({
    items:[button],
    top: 0
});
win.add(toolbar);

var label = Ti.UI.createLabel({
  color: 'white',
  font: { fontSize: 14 },
  text: '点击任一图标，去掉对应的badge。长按进入到编辑模式',
  textAlign: Ti.UI.TEXT_ALIGNMENT_CENTER,
  top: 55,
  height: 40,
  width: 300
});
win.add(label);

var dashboardData = [];
var itemData = [
  { name: 'account', badge: 10 },
  { name: 'cases', badge: 2 },
  { name: 'calls', badge: 2 },
  { name: 'contacts', badge: 5},
  { name: 'emps' },
  { name: 'leads' },
  { name: 'meetings', badge: 3 },
  { name: 'opps',  badge:  126 }, // badge will be displayed as "99+"
  { name: 'tasks' }
];

for (var i=0, ilen=itemData.length; i<ilen; i++){
  var item = Ti.UI.createDashboardItem({
    badge: itemData[i].badge,
    image: '/images/dashboard/' + itemData[i].name + '_off.png',
    selectedImage: '/images/dashboard/' + itemData[i].name + '_on.png',
    label: itemData[i].name
  });
  dashboardData.push(item);
}

var dashboard = Ti.UI.createDashboardView({
  data: dashboardData,
  wobble: true,
  top: 100
});
win.add(dashboard);

var isEditable = false;

button.addEventListener('click', function(e){
  if(isEditable){
    dashboard.stopEditing();
  } else {
    dashboard.startEditing();
  }
});

dashboard.addEventListener('edit',function(e){
  button.title = '完成';
  button.style = Ti.UI.iPhone.SystemButtonStyle.DONE;
  isEditable = true;
});

dashboard.addEventListener('commit',function(e){
  button.title = '编辑';
  button.style = Ti.UI.iPhone.SystemButtonStyle.PLAIN;
  isEditable = false;
});

dashboard.addEventListener('click', function(e){
  e.item.badge = 0;
});

win.open();
```

