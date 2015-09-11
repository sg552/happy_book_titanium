#Icons and Splash Screens(图标和启动图)
这一章节，我们要学习如何在Titanium中自定义设置图标和启动图。当你要提交你的APP给Google Play和Apple Store的时候，对于icon会有很多的要求。Splash Screen（启动图）为了在程序启动的时候，显示一个很重要，很鲜明的信息给用户。

Titanium会给你提供一个默认的icon和一个默认的splash screen给开发出来的项目。但是当你觉得它提供的这个并不好看的话，而且也不符合你的App风格，平台，分发选择的时候，你可以自己创建很多种的图片来覆盖它之前的默认图片。

##你的图片位置
一般情况下，图片文件都能存放在Resources目录。但是，如果你要设置icons（Android和iOS上都叫appicon.png），你可以把对应的图片放到对应的`Resources/android`和`Resources/iphone`目录。如果你要在Android上设置不同分辨率的启动图，你需要把它们分别也放到`Resources/android/images`正确的文件夹里。

Google Play和App Store上都不会把你的图片绑定到你的应用，而是你把图片上传到它们的管理后台中，所以这时候你的图片可是是随意存储，随意命名。

##Pre-rendered icons on iOS
默认情况下，iOS会修改你提交的icon图片，使之成为圆角的并且加上高光，有阴影效果。苹果建议你的icon图是有90度角，没有任何光效果或者光泽效果，也不要用任何透明度。你是无法阻止苹果把你的图标变成圆角，和有阴影的。但是你可以通过在tiapp.xml中来设置一个'prerendered'icon来去掉`reflective shine`。如下：

```xml
<prerendered-icon>true</prerendered-icon>
```

##Build scripts for iOS icons
为了把icon加到你的iOS ipa 文件中，你需要把所有名字正确的文件放到`Resources/iphone`。Titanium的编译脚本会把这些文件复制到最终的ipa包中，之后再等你上传给苹果。

##Splash Screens(启动图)
你可以修改启动图，但你不可以在你的应用加载的时候不要你的启动图。因此你可以简单的把default.png文件给替换掉。你也可以根据不同平台情况，在Resources/xxxx里来替换的。下面是两个平台具体要注意的:

###Android启动图
在Android上，你可以用default.png文件，也可以创建一个nine-patch图片。

自从Android设备有各种屏幕尺寸和屏幕分辨率之后，谷歌就推荐使用nine-patch格式的图片来适配不同的设备。nine-patch文件就是一个具有或者没有伸缩性的png图片。例如，假设你有一个固定背景且中心有logo的图片，这时候你可以创建一个具有伸缩性的nine-patch文件，当它用于适配更大的设备的时候，固定的背景颜色会伸展，但不会对中间的logo产生影响。

做好了这个nine-patch文件之后，命名为dafault.9.png，然后删除掉Resources/android文件夹中的default.png图片。如果同时存在两个文件，编译就会出错。

