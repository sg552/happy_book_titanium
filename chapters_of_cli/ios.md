# ios下的调试

ios 的世界很少有命令行。 大部分时候都是鼠标流。

所以我没有发现特别合适的 等同于 android ADB 的工具。


开发模式下，我们可以看到全部日志

生产模式下，默认你是看不到普通日志的。 可以通过xcode 的organizer 查看Crash Log
(崩溃日志）

- 把iphone连接到 电脑上
- 打开 Xcode -> Window -> Devices
- 选中对应设备
- 点击屏幕左下方的小箭头，可以看到几个小时内的日志。

![查看iphone的日志](/images/iphone_check_log.png)

另外一种解决方案是，把日志专门的写到 iphone的某个文件下。参考：
http://stackoverflow.com/questions/9097424/logging-data-on-device-and-retrieving-the-log
