Welcome to Ti Window World!

如果说，之前提到的View是各种UI元素的container的话，那么Window就是所有View的container。

所以，从这个角度讲，Window是top-level container。

创建一个简单的Window的代码为：
```javascript
var win1 = Titanium.UI.createWindow({
  title:'Tab 1',
  backgroundColor:'#fff'
  });
```

使用Alloy框架创建一个Window的代码为
```xml
<Window title="Tab 1" backgroundColor="#fff">
</Window>
```
