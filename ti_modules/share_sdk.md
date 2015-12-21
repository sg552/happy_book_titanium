国内有一款著名的第三方库——ShareSDK，它封装了第三方分享功能和第三方登录功能，这基本上是一个App的标配，解决了非常普遍的需求。titanium内置没有这些功能，所以我们必须将ShareSDK封装成module。

ShareSDK module在Github上的网址：
```
https://github.com/liumingxing/titanium_module_sharesdk
```
上面有module代码及demo代码，可以仿照demo来进行调用。

第三方分享的示例代码
```
var sharesdk = require("com.mamashai.sharesdk");
sharesdk.addEventListener("share_success", function(e){
	Ti.API.log("分享成功" + e.platform);
})
	
button_share.addEventListener("click", function(e){	
	sharesdk.share({
           title: "分享标题",
           type: "news",
           content: "分享内容",
           url: "http://shareurl.com",
           imageUrl: "http://imageurl.com/test.jpg"
    });
})
```

第三方登录示例代码
```
var sharesdk = require("com.mamashai.sharesdk");
sharesdk.addEventListener("third_login", function(e){
	if (!e.uid && !e.token){
		return;
	}

	var options = {
		uid: e.uid,
		token: e.token,
		nick: e.nickname,
		logo: e.profileImage,
		gender: e.gender,
		platform: e.platform
	}

	if (e.json){
		options.json = e.json;
	}
	http_call({
		url: "http://serverurl.com/api/user/third_login", 
		success: function(e){
			alert(e.responseText)
		},
		method: "POST", 
		args: options
	})
});
login_weixin.addEventListener("click", function(e){
	sharesdk.login({
        tp: "Wechat"
    });
})

login_qq.addEventListener("click", function(e){
	sharesdk.login({
        tp: "QZone"
    });
})

login_weibo.addEventListener("click", function(e){
	sharesdk.login({
        tp: "SinaWeibo"
    });
})
```