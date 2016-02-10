# Android下使用命令行

## android

这个是安卓的自带命令, 用于安装android SDK.

![android manager](/images/android_manager.png)

相信大家对于android SDK很熟悉了，
所以这里的内容不再赘述。

## adb

### 查看日志

只要是在Android  的java代码中，使用了 Log.d() 的语句，就会保存LOG信息，
 就可以通过 `adb shell logcat` 来读取。

这些日志是以 文件的形式，保存在 `/dev/log` 目录下。

verbose/debug/information/warning/error 总共有5种形式。

输入logcat, 然后就会发现，打印出来的都是实时的log.

```bash
shell@android:/ $ logcat
--------- beginning of /dev/log/main
D/wpa_supplicant(  444): wpa_s 0x40f4d7a8 cmd SIGNAL_POLL
D/wpa_supplicant(  444): RX ctrl_iface - hexdump(len=11): 53 49 47 4e 41 4c 5f 50 4f 4c 4c
D/wpa_supplicant(  444): nl80211: survey data missing!
D/wpa_supplicant(  444): ctrl_iface: SIGNAL_POLL
D/wpa_supplicant(  444): wpa_s 0x40f4d7a8 cmd SIGNAL_POLL
D/wpa_supplicant(  444): RX ctrl_iface - hexdump(len=11): 53 49 47 4e 41 4c 5f 50 4f 4c 4c
D/wpa_supplicant(  444): ctrl_iface: SIGNAL_POLL
D/wpa_supplicant(  444): nl80211: survey data missing!
E/BatteryService(  348): set value: false
E/BatteryService(  348): set value: true
E/BatteryService(  348): set value: true
--------- beginning of /dev/log/system
I/ActivityManager(  585): Starting activity: Intent { action=android.intent.action...}
```

它的格式是：

级别-类名-进程pid-具体的信息。  例如：
```
E/BatteryService(  348): set value: true
```
它的级别是 E (Error),  对应的Class是 BatteryService, 对应的pid 是348，具体
的日志信息是 "set value: true"

上面打印的都是 /dev/log 下的文件， 现在看来，有这么几个文件：

```
shell@android:/dev/log $ ls -al
crw-rw-rw- root     log       10,  47 2015-04-11 14:08 events
crw-rw--w- root     log       10,  44 2015-04-11 14:08 exception
crw-rw--w- root     log       10,  48 2015-04-11 14:08 main
crw-rw--w- root     log       10,  46 2015-04-11 14:08 radio
crw-rw--w- root     log       10,  45 2015-04-11 14:08 system
```

比较奇怪的是， 10, 47,  10, 44 并不是文件的大小， 我们使用 cat 命令可以查看，
但是看到的却是部分乱码. 应该是android 直接把日志给压缩了。

一般说来，手机上安装的应用越多，日志内容就越多，一使用logcat，马上是满屏幕日志
乱飞的感觉。所以过滤信息很重要。

`adb logcat` 自带的过滤功能不太好用，我建议大家 使用 Linux自带的 `grep`命令：

```bash
$ adb shell logcat | grep <关键词>
```

如何查看我的某个app的所有日志？

1. 找到你的app 对应的pid. 例如 BatteryService的 pid是 348：
```
E/BatteryService(  348): set value: true
```
2. 使用 logcat + grep:

```bash
$ adb logcat | grep 348
```

### devices

列出当前电脑上连接到的所有安卓机，包括虚拟的。例如：

```
$ adb devices
List of devices attached
3a3bbc63  device
```

### push

把文件从电脑COPY 到手机上。例如：

```bash
$ adb push 优优宝.apk /storage/sdcard0
```
就会发现 根目录下多了一个 `优优宝.apk` 的文件了。

### pull

把文件从手机COPY到电脑上。用法同push.

### shell

进入到手机的操作系统中。可以输入大部分通用的linux命令，例如：

* ls
* cd
* df
* du
* rm
* cp
* mkdir
* find

等等。对于深入理解安卓开发很有好处。例如，下面是我的三星手机上运行adb shell
中 查看硬盘（df -k )的命令：

```
$ adb shell
1|shell@hlte:/ $ df -k
/mnt/media_rw/extSdCard: Permission denied
/mnt/secure/asec: Permission denied
Filesystem                 Size          Used         Free   Blksize
/dev                 1443232.0K         96.0K   1443136.0K      4.0K
/sys/fs/cgroup       1443232.0K         12.0K   1443220.0K      4.0K
/mnt/secure          1443232.0K          0.0K   1443232.0K      4.0K
/mnt/asec            1443232.0K          0.0K   1443232.0K      4.0K
/mnt/obb             1443232.0K          0.0K   1443232.0K      4.0K
/firmware              65488.0K       5168.0K     60320.0K     16.0K
/firmware-modem        65488.0K      53584.0K     11904.0K     16.0K
/system              2306064.0K    2036612.0K    269452.0K      4.0K
/data               12511116.0K   11348424.0K   1162692.0K      4.0K
/cache                350744.0K       6040.0K    344704.0K      4.0K
/persist                8048.0K       4152.0K      3896.0K      4.0K
/efs                   14096.0K       4336.0K      9760.0K      4.0K
/persdata/absolute      9056.0K       4136.0K      4920.0K      4.0K
/preload               10064.0K       7680.0K      2384.0K      4.0K
```

### 录像

很多时候，你需要把你的app 的演示录制下来。在adb中也是可以的。

```bash
$ adb shell
shell@ $ screenrecord --verbose /sdcard/demo.mp4
# 开始操作手机，就会被录下来了。按Ctrl + C 来结束录制。

shell@ $ exit

# 退出后，回到了 电脑的命令行，就可以把录像pull到本地：
$ adb pull /sdcard/demo.mp4
```

