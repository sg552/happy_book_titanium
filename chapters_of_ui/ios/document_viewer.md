# DocumentViewer

用于在app内部查看文件。

![doc view](/images/ui_ios_document_viewer.png)

```javascript
var win = Ti.UI.createWindow({
    backgroundColor: 'white',
    fullscreen: false
});

// ti_book.pdf 放到 app.js 的同级目录下
doc = Ti.UI.iOS.createDocumentViewer({
  url: 'ti_book.pdf'
});

win.open();
doc.show();
```

DocumentViewer支持显示下面这些格式的文件：

- Microsoft Office(DOC，XLS，PPT)（Office 97-2004）
- Portable Document Format files (PDF)
- Images(JPEG,GIF,PNG)
- Rich Text Format files(RTF)
- HTML 和 XML 文件
- Plain text files
- Comma-sparated value files (CSV)

注意：不推荐在DocumentViewer中使用HTML内容。可以用WebView。

