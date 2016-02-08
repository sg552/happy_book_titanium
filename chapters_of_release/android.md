# 发布 Android 应用

## 生成签名文件

签名文件可以让你方便的升级，让新的apk 包直接替换（覆盖安装）旧的apk文件，
并且可以共享之前的数据目录。

另外，签名文件是一个有效的身份证，能够告诉各大应用商店，你的app 是"正宗的"。

我们知道各大应用商店都是靠package名字来 区分 app的，如果有发现其他人来山寨你，
使用同样的package和 名字，那么它的应用是不会被上架的。


另外，很多第三方服务，都需要到你的签名文件，例如，高德地图，在使用之前，需要你
的app是被 有效的签名文件编译过的。 在你的app 使用高德地图时，如果高德地图服务器
端发现你的app 的签名跟之前留下的不符，那么请求服务就会失败。

所以对于安卓来说，签名很必要。

## 生成签名文件

```bash
$ keytool -genkeypair -v -keystore
    /workspace/android_keys/yuehouse -alias yuehouse -keyalg RSA
    -sigalg SHA1withRSA -validity 33333
# 参数 -validity: 33333天后过期。  对于 google store 需要大于10000天。
记得输入过的密码
```
之后就会发现多个一个文件： /workspace/android_keys/yuehouse

## 查看签名文件的详情(md5等)

用下面的命令:

```bash
$ keytool -list -v -keystore /workspace/android_keys/uubpay
（记得密码要输入正确)
Enter keystore password:

Keystore type: JKS
Keystore provider: SUN

Your keystore contains 1 entry

Alias name: uubpay
Creation date: Feb 7, 2015
Entry type: PrivateKeyEntry
Certificate chain length: 1
Certificate[1]:
Owner: CN=Siweitech, OU=Siweitech, O=Siweitech, L=Beijing, ST=Beijing, C=bj
Issuer: CN=Siweitech, OU=Siweitech, O=Siweitech, L=Beijing, ST=Beijing, C=bj
Serial number: 41049??
Valid from: Sat Feb 07 09:50:08 CST 2015 until: Fri May 14 09:50:08 CST 2106
Certificate fingerprints:
   MD5:  DA:E4:20:38:ED:06:C5:CA:A4:3D:D6:E7:74:B6:??:23
   SHA1: FE:36:CE:BC:D6:CD:49:6A:76:30:9A:82:F8:C7:93:75:C9:A3:??:59
   SHA256: 69:B4:ED:48:96:9B:C2:64:01:9A:1B:AC:5E:52:FF:39:E8:84:24:CC:33:EC:A7:A6:0A:6A:C0:D2:2A:44:??:EF
   Signature algorithm name: SHA1withRSA
   Version: 3

Extensions:

#1: ObjectId: 2.5.29.14 Criticality=false
SubjectKeyIdentifier [
KeyIdentifier [
0000: 44 D5 E9 E6 29 A6 6A 44   A0 CE 0E B3 00 ED 4D 7C  D...).jD......M.
0010: 8D 86 54 ??                                        ..T.
]
]
*******************************************
*******************************************

```

很多时候，第三方服务的平台，只需要你提供签名文件的MD5，就是把上面的
MD5中的值加上去
```
Certificate fingerprints:
   MD5:  DA:E4:20:38:ED:06:C5:CA:A4:3D:D6:E7:74:??:A1:23
```

## Titanium 中给app 做签名

正常的 android 开发中，需要人肉使用  `jarsigner` 来运行命令，

在Titanium中，使用下面的命令：

```bash
# 说明:  --target 以及后面的 -K (签名辅助文件）, -P （签名辅助文件的密码）, -L（别名）  -O (output file) 参数.
$ ti build --platform android --target dist-playstore -K /workspace/android_keys/uubpay -P 你的密码 -L uubpay -O ./build
```

### Titanium中的 “开发模式” 和 “发布模式”

值得一提的是，Titanium有这两个模式。

平时使用的是 开发模式（development mode) , 也就是 上面命令中的 `--target` 的
值，不是"dist-playstore".

开发模式也会使用一个 签名文件，一般是放在 home 目录下。(TODO 需要明确）

很可能这个开发模式的签名文件，在你使用 第三方服务 时，也是要用到。（例如填写到高德地图
中，会让你每次调试都不需要打包，方便我们的开发）

## 准备审核图片，上传apk

安卓各大商场都需要三到四张图片来介绍我们的app商品介绍和详情。

另外，要准备好测试用的用户名和密码。因为审核app的同学每天都忙的要死，没有时间
去注册你的app.

最后，上传apk文件.

国内各大应用商店审核的都特别快，一般来说1~3个工作日必定审核通过。
