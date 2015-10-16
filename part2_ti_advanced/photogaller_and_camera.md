# PhotoGallery and Cameral

##实例

在Titanium中使用相册和相机，异常的简单。下面是一个在实际项目中例子:

###调用了本地的相册：

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

      xhr.open("POST", "http://www.xxx.com/interface/users/change_head_pic");
      xhr.send({
        file: event.media,
        token: "you token here"
      });
    }
  });
};

```

### 调用手机上的camera
调用相机的API和调用本地相册的API非常的像

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
	error: function() {
  		// 调用相机失败的时候的callback
  	}，
	// 自动保存到本地相册
	saveToPhotoGallery: true,
	// 允许对图片进行编辑
	allowEditing: true,
	meidaType: [Ti.Media.MEDIA_TYPE_VIDEO, Ti.Media.MEDIA_TYPE_PHOTO]
});
```
TODO:后续加上相机的使用，以及简单的图片裁剪的代码。
