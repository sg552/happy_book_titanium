## 什么是Titanium

Titanium 是由Appcelerator公司开发的一款开源的跨平台移动开发框架，通过Titanium，我们可以使用Javascript语言开发支持多个平台的移动端产品.如果你读了上边的一句话还不知道Titanium是干什么的，那我就这样告诉你，没有它你要用Java开发Android，用Objective-C or Swift 开发iOS，有了它，你只需要用一套Javascript代码，就能开发Android和iOS两套系统的App(ps:其实Titanium也支持WP和Black Berry！)，是不是对它产生了一些兴趣了？那首先让我们先来了解一下 Titanium 整体的框架体系, 它包括 Titanium SDK tools, Titanium APIs, Appcelerator Studio, Modules.

### Titanium SDK

Titanium SDK tools 包含一个基于Node.js的工具包和一个work with the native SDK tool chains的supporting tools，它会把我们的Javascript 源代码通过内置的 Javascript interpreter(解释器) 连同我们项目中的 assets(资源文件) 编译成 an application binary (二进制文件), 如此，就可以安装到我们的模拟器和手机设备上了。

### Titanium APIs

Titanium API 是一套提供给我们访问原生API的 Javascript-based API. 比如当我们创建一个 Titanium button 的时候，Titanium SDK 实际上是创建了一个 native button 的 proxy(代理), 当我们改变它的样式或者事件的时候, 这个代理会改变相应的(native equivalent)原生当量, 当事件被触发后, 这个代理会bubble them up 到我们的Javascript code.

### Appcelerator Studio

Appcelerator Studio 是 Appcelerator 公司开发的一款基于Eclipse 的IDE(Integrated Development Environment), 它的前身是Titanium Studio, 它可以帮助我们极大的简化开发过程，编码，测试，打包，发布，一个它就够了！

### Modules

Titanium Module 是Titanium的又一强大功能，它的作用是进一步扩展我们的Titanium API，具体做法是将我们想要的功能用native code写好，封装成module，我们的App调用这个module即可。换句话说，只要是原生App能做到的事情，Titanium App都可以做到！Module的另一个好处就是可以将我们用Javascript写的某个功能点封装起来，方便复用(ps:widget也可以做到,后续会详细讲).

## Titanium 的运行机制(Titanium 的实质)

![titanium_framework](http://image.happysoft.cc/image/170/titanium_framework.png)

上图来自于Appcelerator 官网，该图以iPhone和Android两个移动平台为例，描述了Titanium的总体框架结构。首先我们用Javascript调用Titanium APIs把我们想要做的事描述出来，Titanium SDK 会将我们调用Titanium APIs 与 native APIs进行绑定(native bindings)，然后Titanium SDK 内置的JS interpreter 会实时的解释，执行这些能够与 native APIs 进行关联的 Titanium APIs。最后Titanium会根据native OS 的不同，打包成不同的project 和 安装包。
