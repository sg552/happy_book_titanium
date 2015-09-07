#SearchView

Android中用于一个特殊文本框用来写用户要搜索的文本。
`SearchView`给用户提供一个查询的接口，并且提交请求到某个地方。
Search View通常用于在tableview中筛选Row元素。类似于`SearchBar`，你可以在tableview的`search`属性中设置增加一个search view。search view 也可以脱离tableview 来使用。
你也可以把一个具体的SearchView对象当作ListView对象中`Titanium.UI.ListView.searchView`的值。

##使用方法
+ 在js文件中使用`Titanium.UI.Android.createSearchView`方法。
+ 在Alloy中的xml文件中使用标签`<SearchView ns="Ti.UI.Android" platform="android"/>`，注意这里的命名空间，和平台。

##使用例子
```javascript
var win = Ti.UI.createWindow({
    backgroundColor: 'blue',
    fullscreen: false
});

// Use action bar search view
var search = Ti.UI.Android.createSearchView({
  hintText: "Table Search"
});

win.activity.onCreateOptionsMenu = function(e) {
  var menu = e.menu;
  var menuItem = menu.add({
    title: 'Table Search',
    actionView : search,
    icon: (Ti.Android.R.drawable.ic_menu_search ? Ti.Android.R.drawable.ic_menu_search : "my_search.png"),
    showAsAction: Ti.Android.SHOW_AS_ACTION_IF_ROOM | Ti.Android.SHOW_AS_ACTION_COLLAPSE_ACTION_VIEW
});
};

var data = [];
data.push(Ti.UI.createTableViewRow({title:'Apple'}));
data.push(Ti.UI.createTableViewRow({title:'Banana'}));
data.push(Ti.UI.createTableViewRow({title:'Orange'}));
data.push(Ti.UI.createTableViewRow({title:'Raspberry'}));

var tableview = Titanium.UI.createTableView({
  data: data,
  search: search,
  searchAsChild: false
});

win.add(tableview);
win.open();
```

![状态1](http://image.happysoft.cc/image/34/屏幕快照 2015-09-06 下午4.00.52.png)
初始状态

![状态2](http://image.happysoft.cc/image/35/屏幕快照 2015-09-06 下午4.01.10.png)
输入一个字母

![状态3](http://image.happysoft.cc/image/38/屏幕快照 2015-09-06 下午4.01.29.png)
精确输入字母

##Alloy中实现上面的效果
###index.xml:
```xml
<Alloy>
    <Window id="win" backgroundColor="blue" fullscreen="false" layout="vertical">
        <TableView id="tableview" top="10" searchAsChild="false">
            <TableViewRow title="Apple" />
            <TableViewRow title="Banana" />
            <TableViewRow title="Orange" />
            <TableViewRow title="Raspberry" />
        </TableView>
    </Window>
</Alloy>
```

###index.js
```javascript
// use action bar search view
var search = Alloy.createController("searchview").getView();
$.tableview.search = search;
$.win.addEventListener("open", function() {
    $.win.activity.onCreateOptionsMenu = function(e) {
        e.menu.add({
            title: "Table Search",
            icon: (Ti.Android.R.drawable.ic_menu_search ? Ti.Android.R.drawable.ic_menu_search : "my_search.png"),
            actionView: search,
            showAsAction : Ti.Android.SHOW_AS_ACTION_ALWAYS | Ti.Android.SHOW_AS_ACTION_COLLAPSE_ACTION_VIEW
        });
    }
    $.win.activity.invalidateOptionsMenu();
});

$.win.open();
```
