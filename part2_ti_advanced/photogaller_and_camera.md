Welcome to PhotoGallery and Cameral World!

在Titanium中使用相册和相机，异常的简单

下面是一个在实际项目中的一个例子，调用了本地的相册：

```javascript
var openPhotoGallery = function() {
  Ti.Media.openPhotoGallery({
     success: function(event) {
      //这里面使用了前面提到的发送HTTP请求的方法
      var xhr = Ti.Network.createHTTPClient();
      xhr.onload = function(e) {
        var res = JSON.parse(this.responseText);
        Ti.UI.createAlertDialog({
          title: "Success",
          message: "status code" + this.status
        }).show();
      };

      xhr.open("POST", "http://cms.yuehouse.co/interface/users/change_head_pic");
      xhr.send({
        file: event.media,
        token: "you token here"
      });
    }
  });
};

```

TODO:后续加上相机的使用，以及简单的图片裁剪的代码。
