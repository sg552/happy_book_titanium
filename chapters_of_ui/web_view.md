# WebView

使用内置浏览器，加载网页内容。

网页可以来自本地——即手机里面内嵌的HTML代码，也可以来自远程。

值得注意的是，Web View的创建所消耗的资源要大于常规的View的创建。
这是因为，Titanium需要将HTML5的内容完全加载到内存当中去。

![webview](/images/ui_webview.png)

## 例子

```js
var webview = Titanium.UI.createWebView({
  url:'http://www.uubpay.com'
});
var window = Titanium.UI.createWindow();
window.add(webview);
window.open({
  modal:true
});
```

## 软解压和硬解压

Web View 有两个工作模式：硬解压和软解呀。前者解析网页速度更快一些。

使用Web View时，对于比较复杂的页面(js较多)，页面打开一片白。看log也没有发现
出了什么错。

这一般是由于硬解压不能正确解析网页造成的。我们只要把它变成软解压就可以了。

比如，当初优优宝app 使用了第三方在线聊天的web客服，总是打不开，于是我们只要
指定它的borderColor 属性，就会让Web View进入到软解压模式：

```js
var webview = Titanium.UI.createWebView({
  url:'http://www.appcelerator.com',
  borderColor: 'white',
  borderWidth: 2
});
var window = Titanium.UI.createWindow();
window.add(webview);
window.open({
  modal:true
});
```

总之，软解压一直都工作正常，发现硬解压有问题时，要及时的转换到这个模式！
