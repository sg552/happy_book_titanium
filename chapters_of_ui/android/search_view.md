# SearchView

`SearchView`给用户提供一个查询的接口，并且提交请求到某个地方。
Search View通常用于在tableview中筛选Row元素。类似于`SearchBar`，
你可以在tableview的`search`属性中设置增加一个search view。

search view 也可以脱离tableview 来使用。

也可以把具体的SearchView对象当作ListView对象中
`Titanium.UI.ListView.searchView`的值。

## 例子

![search](/images/ui_android_searchview.gif)

```js
var win = Ti.UI.createWindow({
    backgroundColor: 'blue',
    fullscreen: false
});

// 搜索框
var search = Ti.UI.Android.createSearchView({
  hintText: "请输入搜索内容"
});

win.activity.onCreateOptionsMenu = function(e) {
  var menu = e.menu;
  var menuItem = menu.add({
    title: 'Table Search',
    actionView : search,
    icon: (Ti.Android.R.drawable.ic_menu_search ?
      Ti.Android.R.drawable.ic_menu_search :
      "my_search.png"),
    showAsAction: Ti.Android.SHOW_AS_ACTION_IF_ROOM |
      Ti.Android.SHOW_AS_ACTION_COLLAPSE_ACTION_VIEW
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

