# Titanium.UI.TableView

> TODO：此处用的Titanium官方的图片和例子

![android](http://docs.appcelerator.com/platform/latest/images/tableview/tableview_android.png)  | ![ios](http://docs.appcelerator.com/platform/latest/images/tableview/tableview_ios.png) | ![mobileweb](http://docs.appcelerator.com/platform/latest/images/tableview/tableview_mobileweb.png)  | ![windows phone](http://docs.appcelerator.com/platform/latest/images/tableview/tableview_wp.png)
------------- | ------------- | ------------- | -------------
android  | ios | mobileweb | windows phone


在controller中创建Button的例子:

*app/controllers/index.js*

```javascript
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

在view中创建tableview的例子:

*app/views/index.xml*

```xml
<alloy>
    <window id="win" backgroundcolor="white">
         <tableview id="table">
            <tableviewsection id="sectionfruit" headertitle="fruit">
                 <tableviewrow title="apple"/>
                 <tableviewrow title="bananas"/>
           </tableviewsection>
           <tableviewsection id="sectionveg" headertitle="vegetables">
                 <tableviewrow title="carrots"/>
                 <tableviewrow title="potatoes"/>
            </tableviewsection>
         </tableview>
    </window>
</alloy>
                                                                                                                                                        <tableviewrow title="cod"/>
                                                                                                                                                                        <tableviewrow title="haddock"/>
                                                                                                                                                                                    </tableviewsection>
                                                                                                                                                                                            </tableview>
                                                                                                                                                                                                </window>
                                                                                                                                                                                                </alloy>
```
