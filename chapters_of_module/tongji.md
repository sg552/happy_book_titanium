统计是app开发中不可或缺的组件，Titanium内置有统计功能。但此项功能属于Titanium的增值服务项，功能受限，若要享受完整的功能需要付费。

Github上有开源的flurry module，可免费享受flurry统计完整的功能。网址：https://github.com/appcelerator-modules/ti.flurry

使用刚起来也非常简单，在app初始化的时候，调用如下代码
```
var Flurry = require("ti.flurry");
Flurry.initialize("API_KEY");
```
其中的API_KEY是从flurry官网申请得到的key

对于ios需要多加一行代码
```
Flurry.reportOnClose(true);
```
保证app退出的时候将数据发送给统计服务器

要记录某个事件的时候，只需要调用如下代码：
```
Flurry.logEvent(event_name,parameters);
```

其中parameters经过我的实验发现没什么具体作用，只需要传第一个参数即可。