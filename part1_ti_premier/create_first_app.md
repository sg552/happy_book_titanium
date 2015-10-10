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
