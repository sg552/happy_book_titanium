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

对于具体分辨率的启动图，你需要把你的nine-patch图片拷贝到你项目的根目录下的`./platform/android/res/drawable[-xdpi]/`，xdpi能够适配多种不同屏幕分辨率，或者使用放到后缀为［－nodpi］的文件夹中来适配所有的屏幕。记得把文件的名字改为background.9.png，例如下面这样：

```
SampleProject
├── app
├── platform
│   └── android
│       └── res
│           ├── drawable-ldpi
│           │   └─── background.9.png
│           ├── drawable-mdpi
│           │   └─── background.9.png
│           ├── drawable-hdpi
│           │   └─── background.9.png
│           └── drawable-xhdpi
│               └─── background.9.png
├── Resources
└── tiapp.xml
```
注意：不要把启动图放在drawable目录下（没有后缀的），因为Android可能会对它进行错误的压缩。如果你想用一张图片来适用整个app，那就把它放到`drawable-nodpi`下。

####Splash Screen with a Custom Theme(自定义主题的启动图)
如果你想给你的启动图添加一个自定义主题的话，覆盖默认的root activity来使用自定义主题：

+ 在`./platform/android/res/values/`目录下创建一个xml主题文件。不要给它命名成`theme.xml`。Titanium在编译的时候，把这个当作它默认的主题文件。如果你创建了一个文件叫作theme.xml，这个新建的文件就会覆盖Titanium默认的theme文件，并且会破坏编译。添加一个使用nine-patch的图片的windowBackground添加到自定义主题里。

  注意：只把windowBackground items添加到这个主题的默认root activity。如果你添加到别的主题去了的话，这个图片可能无法显示。

platform/android/res/values/mytheme.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
<!-- Prior to Release 3.3.0, use a base Holo, Light or Black theme as the parent -->
<style name="Theme.MyTheme" parent="Theme.AppCompat">
    <item name="windowBackground">@drawable/background</item>
    <item name="android:windowBackground">@drawable/background</item>
</style>
</resources>
```

+ 当你生成了`build/android/Androidmanifest.xml`，编译你的应用。打开这个文件可以看到<activity>标签内包含着你默认的root activity，<android:name attribute>中包含着你应用的名字：

build/android/AndroidManifest.xml
```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android" package="com.example.sample" android:versionCode="1" android:versionName="1.0">
  <uses-sdk android:minSdkVersion="14" android:targetSdkVersion="19"/>
  <application android:icon="@drawable/appicon" android:label="AlloyNinePatch" android:name="AlloyninepatchApplication" android:debuggable="false" android:theme="@style/Theme.AppCompat">
    <activity android:name=".YourapplicationnameActivity" android:label="@string/app_name" android:theme="@style/Theme.Titanium" android:configChanges="keyboardHidden|orientation|screenSize">
      <intent-filter>
        <action android:name="android.intent.action.MAIN"/>
        <category android:name="android.intent.category.LAUNCHER"/>
      </intent-filter>
    </activity>
    <activity android:name="org.appcelerator.titanium.TiActivity" android:configChanges="keyboardHidden|orientation|screenSize"/>
    <activity android:name="org.appcelerator.titanium.TiTranslucentActivity" android:configChanges="keyboardHidden|orientation|screenSize" android:theme="@style/Theme.AppCompat.Translucent"/>
    <activity android:name="ti.modules.titanium.ui.android.TiPreferencesActivity" android:configChanges="screenSize"/>
  </application>
  <uses-permission android:name="android.permission.INTERNET"/>
  <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
  <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
  <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
  <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
  <uses-permission android:name="android.permission.ACCESS_MOCK_LOCATION"/>
</manifest>
```

+ 复制默认的root activity到你tiapp.xml中的Android部分的<application>中，你需要在<android>标签对中添加<manifest>和<application>标签对，在这个activity的`android:theme`属性中用你的自定义主题的名字替换掉Theme.Titanium。

tiapp.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<ti:app xmlns:ti="http://ti.appcelerator.org">
    ...
    <android xmlns:android="http://schemas.android.com/apk/res/android">
        <manifest>
            <application>
                <activity android:name=".YourapplicationnameActivity" android:label="@string/app_name" android:theme="@style/Theme.MyTheme" android:configChanges="keyboardHidden|orientation|screenSize">
                    <intent-filter>
                        <action android:name="android.intent.action.MAIN"/>
                        <category android:name="android.intent.category.LAUNCHER"/>
                    </intent-filter>
                </activity>
            </application>
        </manifest>
    </android>
    ...
</ti:app>
```

当你创建一个新的应用，默认地，Android使用名字叫`default.png`的文件作为启动图。你设置的图片文件的大小，尺寸和目标设备的屏幕差别很大。这些特点相当于用户设备的分辨率的大致尺寸。在Resources/android/images文件夹中，你能发现很多类似于`res-long-land-hdpi`的文件夹。

Titanium提供默认的，合适的启动图，放在Resources/android/images下的各个目录下。你可以按照它们的尺寸来简单的创建一个你自己的启动图。如果你不想做各种特定尺寸的适配的话，你可以删掉那些文件夹。然后只把一个default.png文件放在Resources文件夹下或者放在Resources/android下来适配大多数比较接近你设置的尺寸的设备。但是要注意的是：结果可能是在你的设备上，启动图被拉伸或者压缩了。

注意：不要用`<supports-screens/>`元素和任何`android:anyDesity`属性来设置不支持多屏幕适配。Google不建议修改默认的值，如果设置了不支持的话可能造成无法估计的后果。


##iOS graphic asset requirements and options
iOS中的各种图片和Android是有很多大的不同的。所有的图片都必须是PNG格式的，如果不是的话，都会被忽略掉。
对于使用了Alloy的项目，把图片们都放在`app/assets`，`app/assets/iphone`或者`app/assets/ios`文件夹下。
如果是经典模式下的Titanium项目，把文件放在`Resources`，`Resources/iphone`，`Resources/ios`文件夹下。

对于所有的icon文件（文件前缀叫appicon的），这些图片是需要是正方形，也是就是说宽和高是一样的。如果你没有任何的appicon文件，但是有文件叫作`appicon.png`或者`appicon@2x.png`（尺寸至少是180x180）的话，TitaniumSDK会通过这个生成任何丢失的文件。如果你缺少任何icon文件的话，编译会失败。对于用来编译的图片文件（图片文件前缀是Default的），如果缺少任何一个，编译都不会失败。

下面的这个表就是描述了在Titanium中iOS的各种图片的各种要求：

iOS Device | Purpose | Demensions | DPI | File name
--- | --- | --- | --- | ---
iPhone 4/4S/5/5C/5S/6 iPod touch 5th generation | App icon | 120 x 120 | 72 | appicon-60@2x.png
iPhone 6 Plus | App icon | 180 x 180 | 72 | appicon-60@3x.png
iPad non-retina | App icon | 76 x 76 | 72 | appicon-76.png
iPad retina | App icon | 152 x 152 | 72 | appicon-76@2x.png
Universal non-retina | Spotlight | 40 x 40 | 72 | appicon-Small-40.png
Universal retina | Spotlight | 80 x 80 | 72 | appicon-Small-40@2x.png
iPhone 6 Plus | Spotlight | 120 x 120 | 72 | appicon-Small-40@3x.png
Universal non-retina | Settings | 29 x 29 | 72 | appicon-Small.png
Universal retina | Settings | 58 x 58 | 72 | appicon-Small@2x.png
iPhone 6 Plus | Settings | 87 x 87 | 72 | appicon-Small@3x.png
iPhone 4/4S | Splash screen | 640 x 960 | 72 | Default@2x.png
iPhone 5/5C/5S iPod touch 5th generation | Splash screen | 640 x 1136 | 72 | Default-568h@2x.png
iPhone 6 | Splash screen | 750 x 1334 | 72 | Default-667h@2x.png
iPhone 6 Plus landscape | Splash screen | 2208 x 1242 | 72 | Default-Landscape-736h@3x.png
iPhone 6 Plus portrait | Splash screen | 1242 x 2208 | 72 | Default-Portrait-736h@3x.png
iPad non-retina landscape | Splash screen | 1024 x 768 | 72 | Default-Landscape.png
iPad non-retina portrait | Splash screen | 768 x 1024 | 72 | Default-Portrait.png
iPad retina landscape | Splash screen | 2048 x 1536 | 72 | Default-Landscape@2x.png
iPad retina portrait | Splash screen | 1536 x 2084 | 72 | Default-Portrait@2x.png
any device with a non-retina display for ad-hoc builds | app list in itunes | 512 x 512 | 72 | iTunesArtwork (no extension)
any device with a retina display for ad-hoc builds | app list in itunes | 1024 x 1024 | 72 | iTunesArtwork@2x (no extension)

##iTunes Connect Assets
在提交应用到苹果商店的时候，也会有很多的要求，你需要提交至少一张你应用所支持的所有设备上的截图。截图中不能有status bar。下面的表格是对这个的一个总结：

iTunes Connect graphics | Purpose | Demensions | DPI | File name | Specs
--- | --- | --- | --- | --- | ---
One(1) required | Large app icon | 1024 x 1024 | 72 | any | JPG or PNG, flattened, no transparency
One(1) required | iPhone 4/4S screenshot | fullscreen: 960x640 or 640x960  no status bar: 960x600 or 640x920 | 72 | any | JPG or PNG, flattened, no transparency
One(1) required | iPhone 5/5C/5S and iPod 5 screenshot | fullscreen: 1136x640 or 640x1136  no status bar: 1136x600 or 640x1096 | 72 | any | JPG or PNG, flattened, no transparency
One(1) required | iPhone 6 screenshot | 1334x750, 750x1334 | 72 | any | JPG or PNG, flattened, no transparency
One(1) required | iPhone 6 Plus screenshot | 2208x1242, 1242x2208 | 72 | any | JPG or PNG, flattened, no transparency
One(1) required | iPad screenshot | non-retina, fullscreen: 1024x768 or 768x1024  non-retina, no status bar: 1024x728 or 768x1004  retina, fullscreen: 2048x1536 or 1536x2048  retina, no status bar: 2048x1496 or 1536x2008 | 72 | any | JPG or PNG, flattened, no transparency


Titanium之前的一些较早的SDK对于iOS的图片资源已经不提供支持了，所以这里不写了。想看的话，可以去官方文档看。
