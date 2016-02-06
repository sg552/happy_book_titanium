#Titanium.UI.WebView

Web View在Titanium中的作用，是加载基于HTML5的内容。

HTML5的代码，可以来自本地——即手机里面内嵌的HTML代码，也可以来自远程。

值得注意的是，Web View的创建所消耗的资源要大于常规的View的创建。这是因为，Titanium需要将HTML5的内容完全加载到内存当中去。

简单的创建Web View的代码为：
```javascript
var webview = Titanium.UI.createWebView({url:'http://www.appcelerator.com'});
var window = Titanium.UI.createWindow();
window.add(webview);
window.open({modal:true});
```

如果使用Alloy框架的话，代码为：
```xml
<Alloy>
<Window id="win" modal="true">
<WebView id="webview" url="http://www.appcelerator.com" />
</Window>
</Alloy>
```

更多的Web View的内容，敬请期待。
