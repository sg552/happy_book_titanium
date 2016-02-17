# sharesdk

titanium关于sharedsdk module的使用

明星的module地址:https://github.com/liumingxing/titanium_module_sharesdk

首先对于你的应用，你需要知道

安卓
你需要知道你的APP签名字符串，详见:http://doc.tidev.in/part2_ti_advanced/android_release.html

iOS
你需要知道你的APP的 Apple ID 和Bundle ID

新浪微博

去http://open.weibo.com注册自己的应用，审核通过后你会得到你想的App Key和App Secret

此时不要着急关闭该网页，你还需要去接口管理->申请权限->申请高级写入权限（否则分享的时候不能分享图片),然后去应用信息->高级信息，把授权回调页和取消授权回调页写上（写一个可以访问的网址即可）

微信

去http://open.weixin.qq.com注册自己的应用，如果你需要微信支付功能，需要注册完后在管理界面再次申请，审核完成你会得到App ID和App Secret

QQ

去http://open.qq.com注册自己的应用，审核通过你会得到你的App ID和App Secret

此时把目光转向mob.com,就是sharesdk的配置

安卓
添加你的安卓版本App,然后在左侧打开社会化平台设置，你会看到各个分享平台。然后点开新浪微博，填入App Key、App Secret和授权回调页（必须和你在新浪开发平台填写的一致），把状态打开；QQ空间、微信、微信朋友圈、微信收藏，都填入App ID和App Secret，把状态打开

网页端配置完毕，目光转向你的项目，你需要在tiapp.xml中加入这么一个属性 你的mob的App Key,这样就设置安卓的分享就设置完毕

iOS
打开项目的modules->iphone->com.mamashai.sharesdk->3.1->assets->ShareSDK.plist文件，基本配置方法和你在网页上一致，需要把你的App ID或App Key和App Secret填入对应的属性中即可，注意RedirectURL一定要填写

然后用xcode把build->iphone->Info.plist打开，在URL types->URL Schemes中加入微信和QQ的App ID，如下图所示


然后把这个Info.plist复制到项目根目录下

注意问题



-===========  摘自明星的整理

明星给我的sharesdk的讲解，粗糙记录。 回头我整理一份详细的。




在 open.weixin.qq.com 上，创建移动应用



tech@uubpay.com   UUBpay123



android: 给出md5之后， 会得到 appid  appsecret.  （通过审核后）



支付的话，还要再申请一次。



sharesdk:

微信开放平台：https://open.weixin.qq.com，tech@uubpay.com UUBpay123

刘明星  09:53:34

sharesdk www.mob.com  liumingxing@uubpay.com uubpay123



添加应用：  ios , android 各一个。

appkey , appsecret 各一个。  key 是关键。

社会化平台设置，  找到 ： 几个最重要的。（QQ,微信，微博）

在 shards 中：设置好: appid, app key  ， 授权回调页比较重要（之前的 openurl 参数）

其他内容都可以忽略。(默认设置就可以）





进入到tiapp:  把sharesdk module加进来。



android ： 不用配置, 新页面 打开于老页面的上面，所以不用配置。



info.plist    配置 url types. 这个是为了iOS:

iOS: 授权：  tencent1104943450   (这个代表了你的 app id）， com.uubpay.client 设置好之后，就知道分享后如何跳回来了。



iOS: 3.1  编辑：   com.mamashai.sharesdk/3.1/assets/sharesdk.plist

里面的 redirect url 都要设置，设置成sharesdk.cn ，几乎用不上，但是必须有。



(

代码文件放在   com.mamashai… 下面



资源文件，必须放在 tiapp目录下的 platform/ios  下：  （iOS不行， android可以）

platform 下：

android

iphone 下的文件，全都复制过去。



)



info.plist 必须在本地配置，所以 iOS 的 sharesdk.plist也要在本地配置（iOS的配置都在本地）

服务器端的配置优先级最高， 然后sharesdk才会读本地配置。（如果没有服务端，才会读本地）



android:

在tiapp.xml 中，加了：  sharesdkkey 就可以。



微博特别重要。  分享之后，有来自于XXX

微博开放平台，有很多强大的SDK   （  交通路线，poi。。等等）



在android平台下，对于微信的分享，一定要打上证书。  (要在 发布模式  ( deploytype=product) 下，才能用。  ）

ios打到真机上就行。



具体的用法：


```javascript
sharesdk = require "com.mamashai.sharesdk"
sharesdk.addEventListener "share_success", (e)->
    show_alert("分享成功", e.platform)
shares_this_case =  ->
    sharesdk.share
        title: '匠优家家装',
        type: "news",
        content: "您装修的首选",
        url: "http://jiangyoujia.com/share/#{decorating_case_detail_id}",
        imageUrl: Ti.App.advertisement_image

if Ti.App.is_iphone || Ti.App.is_ipad
    //声明一个button
    rightButton = Ti.UI.createButton
        title :"分享"
        color:"#fff"
        font: fontSize:__l(9)
    win.setRightNavButton rightButton

    //为这个button增加分享功能。
    rightButton.addEventListener 'click', (e) ->
        shares_this_case
else if Ti.App.is_android
    add_default_action_bar win
    add_default_action_bar2 win, "项目详情", "分享", shares_this_case
```
