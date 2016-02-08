# 发布 iOS App

IOS的发布过程跟 android 本质一样，实际操作起来略有差别。主要在于ios有两个
文件：

- certificate file （证书）
- provisioning file （授权文件）


另外，ios app有三种不同的打包方式：

- 开发模式下，打包并安装到实体机/虚拟机上。
- 发布到app store之前，内测时，发布到第三方的市场上(例如蒲公英(http://pgyer.com))
以方便其他测试设备的下载
- 正式打包, 为了发布到app store.

## 获取证书和授权文件

- developer.apple.com -> member center

主要获取 App ID，制作各种 certificate （证书），添加 iOS 设备以及配置
provisioning file

- itunesconnect.apple.com

在这里，我们提交 app 给 Apple 审核，并能看到审核后的结果和反馈信息。

## 建立app id.

就是为 App 取一个独一无二的名字

App ID 是识别不同应用程序的唯一标示符。像身份证一样，每个 app 都需要一个 App ID
来唯一标识自己。目前有两种类型的 App 标识：一个是精确的 App ID(explicit App
ID)，一个是通配符 App ID(wildcard App ID)。

使用通配符的 App ID 可以用来构建和 安装多个程序。尽管通配符 App ID 非常方便，但是一个精确的 App ID 也是需要的，尤
其是当 App 使用 iCloud 或者使用其他 iOS 功能的时候，比如 Game Center、Push
Notifications 或者 IAP。在这里，我们使用的是精确的 App ID(explicit App ID)。

关于两种不同 App ID 的区别，可以参考 Apple Technical Note QA1713
https://developer.apple.com/library/ios/qa/qa1713/_index.html

如何产生并指定一个 App ID 给 App 呢？

我们首先要在 Apple 的平台上创建一个 App ID，

在 developer.apple.com -> member center -> iOS Apps -> Identifier

## 签名和证书

为代码签名可以使操作系统识别某个 app 的开发（发布）者是谁（私钥的用
途），也可以保护代码不会被篡改（公钥的用途）。

代码签名使用的是 Apple 提供的一个公私钥对来完成的。公钥保存在证书里面，
证书存放在 member center 里。私钥是在制作证书时候，由程序从你的
login keychain 里面产生的。要想完成对代码的签名，就要同时拥有证书和制
作这个证书的电脑（人）的身份识别信息（也就是私钥）。证书只有和对应的
私钥配对存放在开发者的 keychain 内，开发者才能用这个去签名代码。

可以想象成，只有签了字的支票才能兑现，只有签字过的合同才有法律效力一样。
这里的‘字’就是身份识别信息（也就是私钥）， 证书本身就是一个公钥。

证书分为两种 - Development（开发）和 Distribution（发布）证书。

开发证书用于识别组中的单个成员，这个证书主要用于开发和测试过程中。每次被开
发或被测试的程序都要被这个证书签名一次，编译打包后，只能安装在有限的
（provisioning profile 中指定）设备上。发布证书用于识别一个组，主要用
于编译打包一个要上传到 app store 上的 app，故其名称叫做发布证书。

制作各种不同证书的方法是基本上相同，以制作一个开发证书为例：

a) 进 入 developer.apple.com -> member center 后，选择 Certificates ，
Identifiers & profiles。再在 iOS Apps 下选择 Certificates

b) 点击“+”。下图中可以看出，这个账户在一个 team 中（一个账户可以属于
多个 Team，只要 Team 邀请，用账户的 email 接受邀请即可）已经有了
一个发布证书。

c) 如果想制作开发证书，选择“iOS App Development”。如果想选择分发证
书，选择“In-House and Ad Hoc”。

d) 按照提示，获取开发者身份识别信息（主要就是私钥）并保存此信息到
CSR 文件中。

e) 按照提示，上传 CSR 文件。Apple 会产生对应的证书（公钥），供用户下
载。

以上就完成的证书的制作。开发者想要完成对 App 的签名，就要

- 登陆到 member center 下载该证书
- 通过在 keychain 中导出 p12 文件的形式，获得对应证书的私钥。

## 添加测试设备（对于非企业账号）

如果你的开发者账户不是企业账号，Apple 只允许你的 app 最多安装到 100
个 iOS 设备上。可以被安装的设备需要在这里先添加成为候选设备，再在
provisioning profile 中指定为可下载设备。

- 连接设备到 iTunes。通过 iTunes, 获得 iOS 设备的 UDID
- 进入 developer.apple.com，选择 Devices
- 可以一次只添加一个设备（Register Device），或者做批量添加（Register
Multiple Devices）

## 制作 Provisioning Profile

Provisioning Profile 实际上是个配置文件。他用来告诉 Xcode，一个 app（App
ID）应该用什么有效的证书来签字，可以在哪些设备上安装这个 App。所以，
在制作一个 Provisioning Profile 的时候，我们要指定的是

- App ID
- 可以安装这个 App 的设备（如果是非企业账号）

## 发布形式一：打包并安装到实体机

需要在 Ti 中做的配置

下载好了 Certificates 和 Provisioning Profile 之后，我们就可以连接真机进行测
试了。

- 将测试机连接到电脑上，进入项目根目录，打开 tiapp.xml,
保证<id>和你在 developer.apple.com 中注册的 App Id 一致
- 输入 $ ti info -t ios 这里会列出所有本机关于iOS的配置信息
- 查看Connected iOS Devices 测试机是否已连接上
- 测试机连接成功后，复制 UDID 号，输入

```bash
$ ti build --platform ios --target device --device-id <设备的 UDID>
```

- 选择你的 Development Certificates
- 选择你的 Provisioning Profile
- 执行下面的命令, 就把我们的 App 安装到了实体机上了

## 打包方式二：打包放到内测app的平台：

```
$ti build --platform ios --target dist-adhoc
```

- 上传ipa文件 http://pre.im/ or http://www.pgyer.com/


## 发布形式三：打包并发布到 app store上。

为了上架 Apple Store,需要在 Xcode 以及 Ti 中需要做配置,以及最后的打包
及上传到 iTunesConnect 的过程

- 上架之前,需要设置 App 的 icon 和引导图,进入项目根目录下的 app/assets/iphone/,
按照下图说明将默认的图片替换为自己 App 的相关图片
- 上架到 App Store 与 真机测试的不同之处是: 你下载的证书要是
distribution certificate,如果这个证书不是你创建的,你需要找创建这个证书的
人提供一个 p12 文件给你作为证书的私钥,然后生成一个用于发布的
provisioning profile.下载下 来。
- 进入项目根目录,输入

```bash
$ ti build --platform ios --target dist-appstore
```

- 选择发布证书,以及对应也这个证书的provisioningprofile
- 成功之后会生成一个.ipa文件,打开xcode,点击顶部Windowtab ->Organizer
- 点击 Archive ,这里记录着所有你打包过的 ipa 版本,选择最新的一个打包版 本,
点击 Validate,用来检查一下是否有错误,是否符合苹果上传 ipa 规定,如果验
证成功,最后会提示你 Successful.这时我们就可以点击 Submit 提交到
 iTunesConnect 构建版本中。
- 如果 Submit 成功,打开 http://itunesconnect.apple.com,进入我的 App,
打 开项目,有一个构建版本,点击旁白的 + 号,选择刚才构建好的版本,点击右上角
的提交以供审核就完成了 App 的发布,等待 App Store 审核,
审核成功后可以在 App Store 下载了。

## 注意事项

对于企业开发者账号，测试设备的上线是1000个。

### 增加一个新的测试设备的基本步骤：

- 进入到 apple developer center,
- 进入到编辑 provisioning file的页面
- 找到设备的UUID， 放到device list中， 于是对应的provisioning file会被自动更新。
- 下载最新的provisioning file
- 重新打包app, 发布。

### 新增了测试设备，provisioning file 更新后，老的证书打包的app会闪退。

这个问题无解。

### 填写app的名字时，最好详细的写出的app的内容。

TODO: 例如uub

好的内容可以让你的APP 名列前茅
