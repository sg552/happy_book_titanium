# Titanium.UI.DashboardView  &&  Titanium.UI.DashboardItem（Only IOS）

##介绍

DashboardView和DashboardItem是IOS的特殊组件,DashboardView包含多个DashboardItem而组成一个Dashboard,如下图所示:

![Dashboard](http://image.happysoft.cc/image/19/dashboard.png)

DashboardView里面的东西会以3x3的样式在DashboardView中展现,当超过9个的数量时,会以第二页的形式存储在一个scrollableView中

下面是官方的示例代码,所用到的图片来自KitchenSink [dashboard](https://github.com/appcelerator/titanium_mobile/tree/master/demos/KitchenSink/Resources/images/dashboard)并存放在本地目录*app/assets/images/dashboard*下面:

* 在controller创建的方式:

```javascript
var win = Ti.UI.createWindow({
    backgroundColor: '#13386c'
});

var button = Ti.UI.createButton({
    title: 'Edit',
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
  text: 'Click an item to reset badge\nPress and hold an item to enable edit mode',
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
  button.title = 'Done';
  button.style = Ti.UI.iPhone.SystemButtonStyle.DONE;
  isEditable = true;
});

dashboard.addEventListener('commit',function(e){
  button.title = 'Edit';
  button.style = Ti.UI.iPhone.SystemButtonStyle.PLAIN;
  isEditable = false;
});

dashboard.addEventListener('click', function(e){
  e.item.badge = 0;
});

win.open();
```

* view和controller结合的方式创建:

*app/views/dashboard.xml*

```xml
<Alloy>
    <Window id="win" backgroundColor="#13386c">
        <Toolbar id="toolbar" top="0">
            <Items>
                <Button id="button" onClick="changeMode">Edit</Button>
            </Items>
        </Toolbar>
        <Label id="label" color="white" top="55" height="40" width="300">
            Click an item to reset badge\nPress and hold an item to enable edit mode
        </Label>
        <DashboardView id="dashboard" top="100" wobble="true"
            onClick="resetBadge" onEdit="handleEdit" onCommit="handleCommit">
            <DashboardItem image="account_off.png" selectedImage="account_on.png" badge="10" label="account"/>
            <DashboardItem image="calls_off.png" selectedImage="calls_on.png" badge="110" label="calls"/>
            <DashboardItem image="cases_off.png" selectedImage="cases_on.png" label="cases"/>
            <DashboardItem image="contacts_off.png" selectedImage="contacts_on.png" badge="23" label="contacts"/>
            <DashboardItem image="emps_off.png" selectedImage="emps_on.png" label="employees"/>
            <DashboardItem image="leads_off.png" selectedImage="leads_on.png" badge="1" label="leads"/>
            <DashboardItem image="meetings_off.png" selectedImage="meetings_on.png" badge="5" label="meetings"/>
            <DashboardItem image="opps_off.png" selectedImage="opps_on.png" label="opps"/>
            <DashboardItem image="tasks_off.png" selectedImage="tasks_on.png" label="tasks"/>
        </DashboardView>
    </Window>
</Alloy>
```
*app/controllers/dashboard.js*

```javascript
var isEditable = false;

function changeMode(e){
  if(isEditable){
    $.dashboard.stopEditing();
  } else {
    $.dashboard.startEditing();
  }
});

function handleEdit(e){
  $.button.title = 'Done';
  $.button.style = Ti.UI.iPhone.SystemButtonStyle.DONE;
  isEditable = true;
});

function handleCommit(e){
  $.button.title = 'Edit';
  $.button.style = Ti.UI.iPhone.SystemButtonStyle.PLAIN;
  isEditable = false;
});

function resetBadge(e){
  e.item.badge = 0;
});
```

两种方式都可以用，不过仅仅支持IOS的情况下，如果要做双平台的APP,不建议使用它。