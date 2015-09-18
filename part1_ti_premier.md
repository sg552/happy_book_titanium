# Titanium 入门

## 什么是 Titanium

Titanium 是由Appcelerator公司开发的一款开源的跨平台移动开发框架，通过Titanium，我们可以使用Javascript语言开发支持多个平台的移动端产品.如果你读了上边的一句话还不知道Titanium是干什么的，那我就这样告诉你，没有它你要用Java开发Android，用Objective-C or Swift 开发iOS，有了它，你只需要用一套Javascript代码，就能开发Android和iOS两套系统的App(ps:其实Titanium也支持WP和Black Berry！)，是不是对它产生了一些兴趣了？那首先让我们先来了解一下 Titanium 整体的框架体系, 它包括 Titanium SDK tools, Titanium APIs, Appcelerator Studio, Modules, Appcelerator Arrow.

### Titanium SDK

Titanium SDK tools 包含一个基于Node.js的工具包和一个work with the native SDK tool chains的supporting tools，它会把我们的Javascript 源代码通过内置的 Javascript interpreter(解释器) 连同我们项目中的 assets(资源文件) 编译成 an application binary (二进制文件), 如此，就可以安装到我们的模拟器和手机设备上了。

### Titanium APIs

Titanium API 是一套提供给我们访问原生API的 Javascript-based API. 比如当我们创建一个 Titanium button 的时候，Titanium SDK 实际上是创建了一个 native button 的 proxy(代理), 当我们改变它的样式或者事件的时候, 这个代理会改变相应的(native equivalent)原生当量, 当事件被触发后, 这个代理会bubble them up 到我们的Javascript code.

### Appcelerator Studio

Appcelerator Studio 是 Appcelerator 公司开发的一款基于Eclipse 的IDE(Integrated Development Environment), 它的前身是Titanium Studio, 它可以帮助我们极大的简化开发过程，编码，测试，打包，发布，一个它就够了！

### Modules

Titanium Module 是Titanium的又一强大功能，它的作用是进一步扩展我们的Titanium API，具体做法是将我们想要的功能用native code写好，封装成module，我们的App调用这个module即可。换句话说，只要是原生App能做到的事情，Titanium App都可以做到！Module的另一个好处就是可以将我们用Javascript写的某个功能点封装起来，方便复用(ps:widget也可以做到,后续会详细讲).

### Appcelerator Arrow

TODO新出的功能，据说很强大，还没细看

## Titanium 的运行机制(Titanium 的实质)

![titanium_framework](http://image.happysoft.cc/image/170/titanium_framework.png)

上图来自于Appcelerator 官网，该图以iPhone和Android两个移动平台为例，描述了Titanium的总体框架结构。首先我们用Javascript调用Titanium APIs把我们想要做的事描述出来，Titanium SDK 会将我们调用Titanium APIs 与 native APIs进行绑定(native bindings)，然后Titanium SDK 内置的JS interpreter 会实时的解释，执行这些能够与 native APIs 进行关联的 Titanium APIs。最后Titanium会根据native OS 的不同，打包成不同的project 和 安装包。

## 创建你的第一个Titanium App

下面让我们来创建你的第一个Titanium App，这里有两种方式，一种是通过Titanium-CLI 的方式创建(简称键盘流)，一种是通过Appcelerator Studio 的方式(简称鼠标流)，这里只介绍一下命令行操作，因为studio确实不好用，没事就给你卡死，重启，卡死。。，如果你仍然喜欢studio的方式请参考[官网指南](http://docs.appcelerator.com/platform/latest/#!/guide/Creating_Your_First_Titanium_App)

1. 检查安装环境并创建
  
   `$ ti info`  #查看本机titanium环境，保证Node.js,Titanium CLI,Titanium SDK等都安装正确。
    
   `$ ti create` #输入titanium create 命令，依次按提示选择，即可创建成功

2. 创建成功之后就会得到如下的目录结构

   * LICENSE
   * README
   * Resources
   * tiapp.xml
   
   前两个是信息文件，请自行阅读，tiapp.xml是titanium的配置文件，Resources文件夹下就是我们的项目文件了。其中有一个app.js文件，我们可以把我们要做的事写在这个文件中，其他的文件夹下都是资源文件了。这里提供两种开发方式，一种是经典开发模式，即将逻辑代码，样式代码，视图代码，都写在一个js文件中，比如app.js.还有一种是引入Alloy框架，Alloy是一套Titanium的MVC框架，将逻辑代码，样式代码，视图代码分开。两种开发模式均可。
   
   如果要使用Alloy框架
   
   `$ alloy new`
   
   会生成一个名为app的文件夹，在这里MVC有清晰的分层，在相应位置书写代码即可。
   
3. 回到我们的项目根目录下(tiapp.xml文件所在地)，打包我们的titanium App

	iOS:
	
	`$ ti build --platform ios --target simulator --device-id` 

	Android:
	
	`$ ti build --platform android`
	
	enjoy your App !
   
## 官方文档和 KitchenSink

	[Titanium 官方文档](http://docs.appcelerator.com/platform/latest/#!/guide/Quick_Start)
	
	[KitchenSink](https://github.com/appcelerator/KitchenSink) 是Titanium官方推出的UI Demo App,它是对Titanium 所有UI控件的演示效果，一定要看！
	
## titanium 社区介绍

[Titanium中国开发者论坛](http://tidev.in)




