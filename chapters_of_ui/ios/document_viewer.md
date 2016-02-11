#DocumentViewer
DocumentViewer是用于提供在app内部让用户与本地文件进行交互的控件。

通过方法` Titanium.UI.iOS.createDocumentViewer`来创建。调用这个类，能够抛出一个接口来让用户预览文件，比如像预览邮件一样。

DocumentViewer支持显示下面这些格式的文件：

+ Microsoft Office(DOC，XLS，PPT)（Office 97-2004）

+ Portable Document Format files (PDF)

+ Images(JPEG,GIF,PNG)

+ Rich Text Format files(RTF)

+ HTML 和 XML 文件

+ Plain text files

+ Comma-sparated value files (CSV)

注意：不推荐在DocumentViewer中使用HTML内容。如果要的话，可以用Titanium.UI.WebView来显示。

你可以在document viewer中加载文件，也可以在别的应用中用options menu来加载。如果要用options menu的话，你需要指定一个view，并且使用show()方法来固定那个options menu。

在document viewer 中，点击完成按钮来关闭documentviewer，或者点击右边的navigation 按钮来打开options menu，来进行其他的操作，比如打印或者用别的程序打开这个文件。

##例子
```javascript
var win = Ti.UI.createWindow();
// Use a NavigationWindow to create a navigation bar for the window
var navWin = Ti.UI.iOS.createNavigationWindow({window: win});

var navButton = Titanium.UI.createButton({title:'Launch'});
win.RightNavButton = navButton;

var winButton = Titanium.UI.createButton({
    title:'Launch',
    height:40,
    width:200,
    top:270
});
win.add(winButton);

// Create a document viewer to preview a PDF file
docViewer = Ti.UI.iOS.createDocumentViewer({url:'Example.pdf'});
// Opens the options menu and when the user clicks on 'Quick Look'
// the document viewer launches with an animated transition
navButton.addEventListener('click', function(){
    docViewer.show({view:navButton, animated: true});
});
// The document viewer immediately launches without an animation
winButton.addEventListener('click', function(){docViewer.show()});

navWin.open();
```

![](http://image.tidev.in/image/171/iOS Simulator Screen Shot 2015年9月16日 下午3.19.09.png)

![](http://image.tidev.in/image/172/iOS Simulator Screen Shot 2015年9月16日 下午3.21.29.png)

![](http://image.tidev.in/image/173/iOS Simulator Screen Shot 2015年9月16日 下午3.21.42.png)
