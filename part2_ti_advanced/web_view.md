# Titanium中WebView的使用

###为了充分利用平台的原生WebView组件，我们只需要使用ti.ui.webview。这个接口允许我们创建、显示和交互的本地和远程网络内容


####WebView本身高度仅为200密度无关的像素，但整个网页是通过滚动垂直可视。通过将Web内容到屏幕的一小部分，我们能够使用的剩余空间为任何我们想要的东西。我们可以添加本地UI组件，甚至更多的做。一个远程做更有趣的用途是显示移动优化的内容。这是特别有用的内容包含大量的功能，我们将不必为自己的代码。这一杰出的例子是TI。facebook模块，利用facebook的默认登录界面通过WebView认证。
这个例子，还有其他一些，可以在WebView使用案例章节发现。使用本地Web内容与Web视图经常在处理网络内容时，我们要从本地资源中加载它。这允许脱机使用，可以降低WebView加载时间。本网页的内容可以包括HTML，CSS和JavaScript库，甚至。加载本地网页内容的语法与远程的语法相同

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
