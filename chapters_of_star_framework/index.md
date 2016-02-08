# 【年度最干干货】： 明星框架：把app代码写在远程服务器上。

认识明星是我2015年做的最有价值的事，之一  ^_^    。

而明星框架，则是我2015年遇到的最牛逼框架，没有之一。

原理：

把app的代码写到服务器端，然后在app端访问远程界面。 把代码缓存到本地。 使用  eval () 来调用。

这个框架能够实现，在技术上有几种依托：

1. 代码不需要编译。

2. 支持eval 这样的方法

好处是：

1. 不需要编译的等待时间。 这边写了那边立马看到

2. 可以随时随地修改app上的代码。

前景：

这个框架绝对是一种变革

我们把Titanium 看成是 nginx,  则android 就是linux.   我们在linux上写html是不需要编译的， 同理，我写mobile app，骨架部分需要编译， 肌肉部分是不需要的。

过程：

假设你的代码，在titanium上是静态代码:

app.js:
nearby_window = requeir('/lib/nearby_houses.js');

window = Ti.UI.createWindow({
    title: '本地的工地'
})
label = Ti.UI.createLabel({
    text: '这里的内容是本地的，将来要放到远程上'
})
window.add(label)
window.open()
那么，我们要做的是：

1. 先把这个window 在app.js中 抽取出来，成为一个 js module:

app目录下的 /Resources/lib/nearby_houses.js:

Wrapper  = function(){
    window = Ti.UI.createWindow({
        title: '本地的工地'
    })
    label = Ti.UI.createLabel({
        text: '这里的内容是本地的，将来要放到远程上'
    })
    window.add(label)
    return window;
}

module.exports = Wrapper;
2. 在 Resources/app.js 中，使用 require 来调用这个module:

wrapper = require('lib/nearby_houses.js');
wrapper.open()
运行，没问题~

3. 开始分解  nearby_houses.js， 把它的内容从远程调用：

Wrapper = ->
    Ti.include '/lib/public.js'

    window = Ti.UI.createWindow
        title: '附近的工地'

    setup_window = ->

        http_call
            url: Ti.App.householder_code_url + "/householder_code/nearby_houses.js"
            cache: true
            success: (e) ->
                console.info "== got code successfully"
                some_window = eval(e.responseText)
                some_window(window)

            // 下面部分的代码，是当网络不好时，生成一个消息提示，并且给个按钮，让用户重新下载代码。
            error: () ->
                window.add Ti.UI.createLabel
                    top: __l(100)
                    text: '哎呀，网络连接似乎有点问题！'
                    textAlign: 'center'
                    font: fontSize: __l(18)
                    color: '#333'

                button = Ti.UI.createButton
                    title: "重试"
                    top: __l(150)
                    width: __l(80)
                    font:
                        fontSize: __l(18)
                button.addEventListener "click", (e) ->
                    setup_window()
                window.add(button)

    setup_window()
    window

module.exports = Wrapper
这个 http_call 的方法看起来这样：( 放到 Resources/lib/public.js 中）

http_call = (options) ->
    if options.cache
        if Ti.App.deployType == "production"
            record = require("/lib/db").db.select_with_check(options.url, 0)
            unless record.blank
                if options.success
                    options.success({ responseText: record.json})

    xhr = Ti.Network.createHTTPClient()
    xhr.timeout = Ti.App.timeout
    xhr.onerror = ->
        if options.error then options.error this else show_timeout_dlg xhr,url
    xhr.onload = ->
        options.success this if options.success
    url = options.url
    if options.url.indexOf(Ti.App.householder_host_url) == 0
        append = "osname="+Ti.App.osname+"&osversion="+Ti.App.osversion+"&appversion="+Ti.App.version+"&manufacturer="+Ti.App.manufacturer+"&model="+Ti.App.model+"&memory="+Ti.Platform.availableMemory
        url += if options.url.indexOf("?") > 0 then "&" + append else "?" + append
    xhr.open options.method || 'GET', url
    if options.args then xhr.send options.args else xhr.send()

对于 lib/db.coffee :

Bizsim = Bizsim or {}
Bizsim.db = {}

Bizsim.db.select_with_check = (json_type, id) ->
  record = Bizsim.db.select_one_json(json_type, id)
  now = new Date
  #数据3天过期
  if Titanium.Network.online and !record.blank and now.getTime() - (record.created_at) > 1000 * 3600 * 24 * 3
    Bizsim.db.delete_one_json json_type, id
    return { blank: true }
  record
Bizsim.db.delete_one_json = (json_type, id) ->
  Ti.App.db.execute 'delete from jsons where json_type=? and id=?', json_type, id
  return
module.exports = Bizsim
同时，你要有个远程服务器，在远程服务器的 /code/nearby_houses.js 中，要返回这个内容：

NearbyHousesWindow = function(window) {
  Ti.include('/lib/public.js');
  label = Ti.UI.createLabel({
    text: '这个Label被放到了远程服务器上'
  })
  window.add(label);
  return window;
};

module.exports = NearbyHousesWindow;
现在，你要修改window的代码的话，完全不需要编译重启app,  直接在远程修改就完事儿了。

几点注意：

1. 一些module ， 不但文件需要放到本地， 代码运行最好也在本地，否则会出现 有时加载不了的情况。 深层原因疑似 网络加载有延迟。 放到本地的话就没有了。

2. 一些方法，需要提前放到一个 匿名js中运行一下。 例如：

$ cat Resources/anon.js
/*
 * 这个文件，系统是不会调用的。
 * 它存在的目的，是为了骗过编译器，(先调用一些API， createTextArea, createOptionDialog)
 * 让编译到实体机时，系统不会出错。
 * Anon 的意思是 Anonymouse
 * */
function AnonWindow(title) {
  var t = Ti.UI.createTextArea({
    hintText: "反馈内容"
  });

  var optionsDialogOpts = {
    title: "选择您想进行的操作",
    options : ["1", "2"],
    cancel : 1
  };

  Titanium.UI.createOptionDialog(optionsDialogOpts);

  Ti.Filesystem.applicationCacheDirectory;

  Titanium.UI.iPhone.TableViewStyle.GROUPED,
  Ti.Geolocation.preferredProvider = "gps";
}

module.exports = AnonWindow;
