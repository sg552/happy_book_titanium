国内有一款著名的第三方库——ShareSDK，它封装了第三方分享功能和第三方登录功能，这是非常普遍的需求，这基本上是一个App的标配。titanium内置没有这些功能，所以我们必须将ShareSDK封装成module。

ShareSDK module在Github上的网址：
```
https://github.com/liumingxing/titanium_module_sharesdk
```
上面有module代码及demo代码，可以仿照demo来进行调用。

ShareSDK有很多的配置工作，需要设置在各个社交平台上的token及secret，比较繁琐。

安卓的配置
```
去sharesdk注册账号，新建一个app，获得key，然后将key写入tiapp.xml中，比如：
<property name="sharesdkkey" type="string">c74ddc6548b5</property>
然后再在sharesdk的官网上将各个平台的token和secret填写进去
```

ios的配置
```
ios配置更加复杂一些，需要配置url_schema，以便微信、QQ被打开后能顺利返回app。
然后将各个社交平台申请到的key和secret填入到ShareSDK module的配置文件，具体路径在modules/com.mamashai.sharesdk/3.1/assets/ShareSDK.plist
```

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
点击按钮后，手机会弹出一个窗体，列出最常用的9个第三方平台，比如微信好友、微信朋友圈、微博、qq好友，qq空间等，用户选择一个平台后，即可将信息分享到指定平台。

可以看到短短几行代码就实现了分享内容到第三方平台的功能，非常方便。

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

可以看到调用出第三方的登录平台是很简单的，比用objc和java进行本地语言开发要简单多了。