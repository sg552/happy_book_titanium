# 相册和相机的使用

Ti.Media 这个class 是关键。

## 相册

下面的例子调用了本地的相册：

```javascript
Ti.Media.openPhotoGallery({
   success: function(event) {
    var xhr = Ti.Network.createHTTPClient();
    xhr.onload = function(e) {
      var res = JSON.parse(this.responseText);
      Ti.UI.createAlertDialog({
        title: "操作成功",
        message: "状态码：" + this.status
      }).show();
    };

    xhr.open("POST", "http://www.uubpay.com/interface/update_avatar");
    xhr.send({
      file: event.media,
    });
  }
});

```

## 调用手机上的camera

```javascript
Ti.Media.showCamera({
  success: function(event) {
    if (event.mediaType == Ti.Media.Media_TYPE_PHOTO) {
      var imageView = Ti.UI.createImageView({
          width: win.width,
          height: win.heigth,
          image: event.media
      })
      win.add(imageView);
    }else {
      alert("你选中的并不是图片");
    }
  },
  error: function() { }，
  // 自动保存到本地相册
  saveToPhotoGallery: true,
  // 允许对图片进行编辑
  allowEditing: true,
  meidaType: [Ti.Media.MEDIA_TYPE_VIDEO, Ti.Media.MEDIA_TYPE_PHOTO]
});
```
