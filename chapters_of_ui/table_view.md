# TableView

TableView 跟 ListView(list_view.md) 一样，都是列表。区别在于后者的性能更好，
前者在样式和表现方面更加灵活。

你的列表中，每一行的样式都完全一样，那么就用ListView.

如果其中某几行的样式跟其他的稍有不同，那么就一定要用TableView.

TableView 由 TableViewSection, TableViewRow组成。

![android](/images/ui_tableview_android.png) | ![ios](/images/ui_tableview_ios.png) | ![wp](/images/ui_tableview_wp.png)
:---:|:---:|:---:
android | ios | windows phone

```js
Ti.UI.backgroundColor = 'white';
var win = Ti.UI.createWindow();

var sectionFruit = Ti.UI.createTableViewSection({ headerTitle: 'Fruit' });
sectionFruit.add(Ti.UI.createTableViewRow({ title: 'Apples' }));
sectionFruit.add(Ti.UI.createTableViewRow({ title: 'Bananas' }));

var sectionVeg = Ti.UI.createTableViewSection({ headerTitle: 'Vegetables' });
sectionVeg.add(Ti.UI.createTableViewRow({ title: 'Carrots' }));
sectionVeg.add(Ti.UI.createTableViewRow({ title: 'Potatoes' }));

var table = Ti.UI.createTableView({
  data: [sectionFruit, sectionVeg]
});

win.add(table);
win.open();

var sectionFish = Ti.UI.createTableViewSection({ headerTitle: 'Fish' });
sectionFish.add(Ti.UI.createTableViewRow({ title: 'Cod' }));
sectionFish.add(Ti.UI.createTableViewRow({ title: 'Haddock' }));

table.insertSectionBefore(0, sectionFish);
```

