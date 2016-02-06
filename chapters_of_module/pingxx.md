开发App的时候，如果遇到用户付款购买的功能需求，那么就必须集成支付宝付款或者微信付款功能，对于要求高的，可能还需要集成银联支付功能。目前国内App开发付款功能最好的选择是采用ping++，官方主页：https://pingxx.com 。ping++封装了各家付款平台的差异性，极大的降低了App集成付款功能的难度。省的程序员去支付宝、微信等各家平台参阅开发资料，极大的节省了程序员的时间。

Github有现成的ping++ module，使用起来很方便，ios和安卓都支持，下载下来直接使用即可。注意：ping++对各家渠道有一些配置工作需要完成，这些工作要在ping++的服务端完成。对于每个付款渠道，只有服务端配置信息完成了，客户端才可以真正的调出该渠道的支付窗体来。

ping++ module在Github上的网址：
```
https://github.com/liumingxing/titanium_module_pingplusplus
```

调用示例
```
var pingpay = require("com.mamashai.pingxx");
pingpay.addEventListener("ping_paid", function(e){
    //code的值可能为success， fail, cancel, invalid, error
    show_alert("提示", "收到了ping_paid信息 code: " + e.code + " text:" + e.text);
});

function ios_resume(e){
    var args = Ti.App.getArguments();
    var code = args.url.split("=")[1];
    pingpay.fireEvent("ping_paid", {code: code, text: ''});
}
Ti.App.addEventListener("resumed", ios_resume);
win.addEventListener("close", function(e){
    Ti.App.removeEventListener("ios_resumed", ios_resume);
});

btn.addEventListener("click", function(e){
    pingpay.pay({
        url: "http://bak.mamashai.com:3000/pay/make_payment",
        order_no: "100023",
        amount: "8",                    //以分为单位
        channel: "alipay",              //可选项为：alipay,wx,upmp,jdpay_wap,百度钱包不支持
        url_scheme: "bizsim"
    });
})
```

参数解释： 

url：ping++需要在服务端进行配置，这个URL接受客户端的付款请求 

order_no：付款之前肯定得先生成订单，付款时传入订单号即可 

amount：订单要付款的金额，以分位单位，不是元 

channel：可选项为：alipay,wx,upmp,jdpay_wap,bfb安卓下百度钱包不支持 

url_scheme：ios下必须传入，付完款后跳回app用的，用xcode打开项目，项目属性->INFO中可以查看，IOS下微信支付对url_scheme参数有特殊要求，详情可见https://pingxx.com/guidance/client/sdk/ios

客户端付完款后，ping++会回调server端的notify url，这个比较简单，不涉及到本地端技术，在notify url中获得详细参数，回填各种信息（比如付款时间，付款是否成功等）到付款记录中即可。

服务端也需要进行一些开发，具体的可以看ping++的官方指南。github上有一个ruby on rails的项目示例。