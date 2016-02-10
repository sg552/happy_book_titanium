# 集合了所有的UI 演示的例子

在看文字之前，我们要先看这个DEMO： KitchenSink.

Kitchensink, 是美国的一句俚语，表示无所不包。

Appcelerator 的CEO 给项目起这个名字，估计跟他的军人经历有关。总之，这里
表示我们所有的UI 都可以在这里得到演示了。

看到了这些UI，你就会对Ti 的UI体系有深刻的了解了 .

1. 下载官方的kitchensink到本地：
```
$ git clone https://github.com/appcelerator/KitchenSink.git
```
2. 编译并运行:
```
$ ti build
```

第一个Tab: "Base UI" , 包含了基本的大类的UI：  Window, TabGroup, Layout等。
![basic tab](/images/kitchen_sink_tab_basic_ui.png)

点击 Base UI tab中的 "Tab Groups", 就可以看到 "Tab Groups"的若干不同用法：
![ui tab](/images/kitchen_sink_tab_group.png)

第二个Tab: "Controls", 所有的输入框，选择，下拉单，搜索框，slider等。
![ui tab](/images/kitchen_sink_tab_controls.png)

第三个Tab: "Phone", 所有跟手机相关的原生功能都在这里：录音，视频，拍照，
重力加速，地理位置信息，摇一摇等等。

![phone tab](/images/kitchen_sink_tab_phone.png)

第四个Tab: "Platform", 包含了绝大部分的高级功能：向服务器发请求，本地存储信息，
事件，数据库等。

第五个Tab: "Mashups", 包含了社交类的信息DEMO。由于后面两个tab中的一些功能用到了
国外的服务器，所以对我们没有太多实用价值，仅供参考。
