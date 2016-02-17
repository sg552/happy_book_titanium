# ProgressBar

用来展示进度。

我们常见的上传或下载进度都可以通过它来实现。

![progressbar](/images/ui_progress_bar.gif)

下面是各个不同平台上的ProgressBar:

![android](/images/ui_progressbar_android.png) | ![ios](/images/ui_progressbar_ios.png) | ![windows phone](/images/ui_progressbar_wp.png)
:---:|:---:|:---:
Android | iOS| Windows Phone

下面是一个静态的进度条的例子：

```js
var pb = Ti.UI.createProgressBar({
  top: 25,
  width: 250,
  min: 0,
  max: 10,
  value: 0,
  color: 'blue',
  message: 'Downloading 0 of 10',
  font: {fontSize: 14, fontWeight: 'bold'},
  style: Titanium.UI.iPhone.ProgressBarStyle.PLAIN,
});
var win = Ti.UI.createWindow({backgroundColor: 'white'});
win.addEventListener('click', function(){
  if (pb.value < pb.max) {
      pb.message = 'Downloading '+ ++pb.value + ' of 10';
  }
});
win.add(pb);
win.open();
pb.show();
```

通过上面的演示案例，我们可以梳理出ProgressBar的一些重要属性:

- min：最小初始值，即进度从哪里开始递增；一般从0开始，也可以设置为其他值，但必须是number型。
- max：最大值，当进度为最大值时进度递增结束。
- value：当前进度
- color：定义的进度值的颜色。
- style：样式类型。在不同的系统平台上，默认样式都是不同的。

进度条通常要与某个操作（例如上传文件）配合使用，才能实时更新进度的百分比。
一般都是在callback中做。例如，在发送http 请求时，对应的callback
就是 `on_send_stream`, 代码如下：

```js
client = new HTTPClient();
client.on_send_stream: function(e) {
  console.info('上传进度：' + e.progress);
  // 可以在这里设置 progressbar的进度：
  my_progressbar.value = e.progress;
}
```

