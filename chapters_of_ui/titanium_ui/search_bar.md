# Titanium.UI.SearchBar

> 此处用的Titanium官方的图片和例子

![android](http://docs.appcelerator.com/platform/latest/images/searchbar/searchbar_android.png)  | ![ios](http://docs.appcelerator.com/platform/latest/images/searchbar/searchbar_ios.png)|
------------- | ------------- |
android  | ios |


在controller中创建Button的例子:

*app/controllers/searchbar.js*


```javascript
var search = Titanium.UI.createSearchBar({
   barColor:'#000',
   showCancel:true,
   height:43,
   top:0,
});
```

在View中创建searchbar的例子:
*app/views/searchbar.xml*

```xml
<Alloy>
    <SearchBar id="search" barColor="#000" showCancel="true" height="43" top="0" />
</Alloy>
```
