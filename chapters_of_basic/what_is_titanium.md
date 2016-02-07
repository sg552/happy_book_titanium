# Titanium 周边产品简介。

## 什么是Titanium

Titanium 是一个框架，或者SDK， 能够把js代码转换成 native android/ios app.
Titanium 是Appcelerator的主力产品。

## Appcelerator 公司简介

从名字上来看，是app + accelerator 的 组合，意为加速app的开发。所做的产品
都是侧重web+app开发的。

两个创始人： Jeff, Nolan, 他俩先在 Jeff 创建的公司认识，然后Jeff卖掉了原来
的公司，建立了 Hakano.  致力于开发web2.0 应用。

2007 年10月，他俩把公司名字改成了Appcelerator.  07年12月， Jboss的创始人
加入，成为公司的顾问。

2008年12月， Titanium 预览版 被开发出来，作为 Adobe AIR的竞争者。同时，
公司收到了 A轮 400万美元的投资。

2009年6月，Titanium beta版出来。

2010年3月，Titanium 1.0 面世。

2010年4月，在Apple与 Adobe Flash的纠纷中， Apple Store下架了所有的 非
native app. （使用某种中间层，特别是phonegap这样的，native app外壳，
里面是 webview ）  当时让大家对 Titanium的前途非常担忧。 不过apple
从未对 titanium app 下手，并且5个月之后，完全允许Titanium 的作品。

2010年10月，titanium 获得了B轮融资 900万。(ebay , sierra )

2011年1月，titanium 收购了 apatana （ Rails 的Eclipse 平台，该小组进而发
布了titanium studio.  ） 然后又收购了 Particle Code, 一家基于HTML5的游戏
公司。 到 2011年10月时，已经有了100个雇员。一年前只有20人。

到2011年11月，Titanium 获得了 1500万美元的 C轮融资。 成为了 Apple Store
和 Android Market 的 最大的第三方开发商。 公司当时的收益是 340万美元。
比2008年 增长  374%

2012年，Titanium 荣获了很多荣誉， 2月份，收购了cocoafish, 一家做service
的公司，后来titanium把它的功能放到了 cloud service 中，就有了push,
upload image等功能。 4月，出现了Titanium 2.0 。

2012年11月。收购了nodable, 一家很大的分析公司（所以 后来就有了自己的统计
平台）

2013年初，《Business Insider》杂志表示，微软有收购appcelerator的意向，
但是后来就没了消息, 估计只是个传言。

2013年5月， appcelerator platform 上线。向企业级移动应用平台进军。

2013年7月，收到了 1210万美元的融资，来自EDBI。 由于EDBI是属于新加坡政府
的投资项目，所以 appcelerator表示要在新加坡亚太总部。

2013年8月，收购了singly. 一家专注于集成API的公司。

2013年10月，hyperloop面世。 hyperloop是使用js语言开发IOS的框架。它会把js
代码非常严格准确的转换成对应的Object-C代码。

2014年8月，获得D轮2200万美元的融资。截至当时，Appcelerator 已经收到了总共9000万美元的投资。

2015年1月， titanium 3.5GA版出现.

2015年5月，Titanium 发布了 4.0.0.GA。

2015年9月，Titanium 发布了 5.0.0.GA。

2016年1月，Titanium 发布了 5.1.2.GA

2016年1月 Appcelerator 被Axway 公司收购。官方表示，所有的Titanium和
Appcelerator 周边产品都不会被影响。我个人通过内部渠道，也得知Titanium
讲继续向前发展。

## Titanium SDK

Titanium SDK tools 包含一个基于Node.js的工具包和一个work with the native
SDK tool chains的supporting tools，它会把我们的Javascript 源代码通过内置
的 Javascript interpreter(解释器) 连同我们项目中的 assets(资源文件) 编译
成 an application binary (二进制文件), 如此，就可以安装到我们的模拟器和手机设备上了。

## Titanium APIs

Titanium API 是一套提供给我们访问原生API的 Javascript-based API. 比如当
我们创建一个 Titanium button 的时候，Titanium SDK 实际上是创建了一个
native button 的 proxy(代理), 当我们改变它的样式或者事件的时候, 这个代理
会改变相应的(native equivalent)原生当量, 当事件被触发后, 这个代理会
bubble them up 到我们的Javascript code.

## Appcelerator Studio

Appcelerator Studio 是 Appcelerator 公司开发的一款基于Eclipse 的IDE
(Integrated Development Environment), 它的前身是Titanium Studio,
它可以帮助我们极大的简化开发过程，编码，测试，打包，发布，一个它就够了！

注意： 不要用它。

## Arrow Cloud, Arrow Builder

提供服务器端的服务。比如提供移动端使用的接口，允许你注册用户等等。

注意： 我们也不用它。

## Analytics, Dashboard

提供专门的后台可以看到各种统计数据，可以发送 PUSH。也可以聊天。

注意：我们也不用它。


为什么不用 Arrow, Cloud service 和 Studio? 因为它们都需要连接到海外的服务
器，会直接影响到网速和用户体验。我们做的任何应用，功能可以少，但是必须
稳定。

## Titanium 的运行机制(Titanium 的实质)

下图以iPhone和Android两个移动平台为例，描述了Titanium的总体框架结构。首先我们用Javascript调用Titanium APIs把我们想要做的事描述出来，Titanium SDK 会将我们调用Titanium APIs 与 native APIs进行绑定(native bindings)，然后Titanium SDK 内置的JS interpreter 会实时的解释，执行这些能够与 native APIs 进行关联的 Titanium APIs。最后Titanium会根据native OS 的不同，打包成不同的project 和 安装包。
![Titanium](/images/titanium_sdk_architecture.png)

# app开发与 web开发的主要区别

我们现在的优势： （只有明星我们知道）

(初期可以不考虑这条）

1. 把代码放在远程服务器上。 这样，就做到了不需要每次都发布app。 修改bug，直接在服务器端修改。

2. 改动瞬间生效。（ 有两个页面。一个页面是第二个页面的入口, （在1#页面点击按钮，进入到2#页面））
我们每次修改2#页面后，退回到1#页面，再点击按钮，2#页面的改动马上就可以看到了！）

3. 不需要做机型适配。 ( 小手机上看起来什么样，大手机就什么样。 16:9 的什么样。

16：10的也按照原比例进行拉伸，所以，看起来是差不多的）

4. 不需要做跨平台的适配（有个前提，大家在使用UI组件的时候，最好使用通用的组件。
）

可以节省我们大量的时间。 让我们的开发变得快乐。

实际的情况：

一天，最多改20次（实际上一天改一个UI 页面就差不多了） 甚至，改一个BUTTON
的样式，都特别痛苦。 黄敏的生产率很高。 但是，他当时调一个页面，需要3天。

开发门槛很高，需要大家具备的能力有：

1. 熟悉所有的UI组件
2. 知道 app 的内在架构（就是通过 event来驱动的，手点点点。。才能看到各种
页面）
3. 知道 如何调用 native的功能。 照相，调用相册，发push 等等。(module)
4. 知道如何调试。 它的调试信息，不如rails可读性那么强。所以大家要具备经验。
5. 每个人都要知道如何编译，打包啊。做到，每天下班前，都要给产品经理一个最新的版本。
6. 使用到了很多js的功能（requirejs -- 拆分的, underscore, coffeescript ... )
