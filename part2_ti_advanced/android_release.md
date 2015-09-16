#Android App 发布

###1.生成签名:
签名可以让你方便的升级，让新的apk 包直接替换（覆盖安装）旧的apk文件，并且可以共享之前的数据目录。所以对于安卓来说，签名很必要。
基本命令是：


```javascript
$ keytool -genkeypair -v -keystore /workspace/android_keys/yuehouse -alias yuehouse -keyalg RSA -sigalg SHA1withRSA -validity 33333
# 参数 -validity: 33333天后过期。  对于 google store 需要大于10000天。
记得输入过的密码
```
之后就会发现多个一个文件： /workspace/android_keys/yuehouse

### 可以用下面的命令查看这个 签名的详情:
$ keytool -list -v -keystore /workspace/android_keys/yuehouse
（记得密码要输入正确)

可以得到结论：  这个签名字符串就是 md5 去掉了： ，并且全小写的结果。
Certificate fingerprints:
   MD5:  DA:E4:20:38:ED:06:C5:CA:A4:3D:D6:E7:74:??:A1:23
   结果为：  dae42038...a123

###2.打包app为apk
```javascript
   正常的 android 开发中，需要人肉使用  jarsigner 来运行命令，在Titanium  中，使用下面的命令：
   # 注意 --target 以及后面的 -K (签名辅助文件）, -P （签名辅助文件的密码）, -L（别名）  -O (output file) 参数.
   $ ti build --platform android --target dist-playstore -K /workspace/android_keys/yuehouse -P xxx -L yuehouse -O ./build
```


###3.准备审核图片,安卓各大商场都需要三到四张图片来介绍我们的app商品介绍和详情。

###4.上传apk到各个安卓市场。

