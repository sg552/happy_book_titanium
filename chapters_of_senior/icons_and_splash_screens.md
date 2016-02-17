# 图标和启动图

当我们要提交APP给各大商店审核的时候，对于图标会有很多的要求。
动图则是可以在程序启动的时候，显示一个很重要, 很鲜明的信息给用户。

## 最佳实践

很多技术的官方文档都对不同的设备尺寸列出了不同的图片尺寸要求。我们的经验是，
不需要这样做。耗时耗力，效果有限，还不如把精力放在更有价值的地方。

确定一张图片，让它自动缩放就好了。

## 图片位置

一般情况下，图片文件都能存放在Resources目录。
但是，如果你要分别设置不同平台的icons（Android和iOS上都叫appicon.png），
你可以把对应的图片放到对应的`Resources/android`和`Resources/iphone`目录。
如果你要在Android上设置不同分辨率的启动图，你需要把它们分别也放到
`Resources/android/images`中对应的文件夹里。


## 启动图

可以修改启动图，但不可以在应用加载的时候不要启动图。
因此你可以简单的把default.png文件给替换掉。

也可以根据不同平台情况，在Resources/xxxx里来替换的。

下面是两个平台具体要注意的:

### Android启动图

在Android上，你可以用default.png文件，也可以创建一个nine-patch图片。

自从Android设备有各种屏幕尺寸和屏幕分辨率之后，谷歌就推荐使用nine-patch格式的
图片来适配不同的设备。

例如，假设你有一个固定背景且中心有logo的图片，
这时候你可以创建一个具有伸缩性的nine-patch文件，
当它用于适配更大的设备的时候，固定的背景颜色会伸展，
但不会对中间的logo产生影响。

做好了这个nine-patch文件之后，命名为dafault.9.png，然后删除掉
Resources/android文件夹中的default.png图片。

如果同时存在两个文件，编译就会出错。

对于具体分辨率的启动图，你需要把你的nine-patch图片拷贝到你项目的根目录下的
`./platform/android/res/drawable[-xdpi]/`，xdpi能够适配多种不同屏幕分辨率，
或者使用放到后缀为［－nodpi］的文件夹中来适配所有的屏幕。

记得把文件的名字改为background.9.png，例如下面这样：

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

注意：不要把启动图放在`drawable`目录下，因为Android
可能会对它进行错误的压缩。如果你想用一张图片来适用整个app，
那就把它放到`drawable-nodpi`下。

### 自定义主题的启动图

如果你想给你的启动图添加一个自定义主题的话，覆盖默认的root activity
来使用自定义主题：

- 在`./platform/android/res/values/`目录下创建一个xml主题文件。
不要给它命名成`theme.xml`。Titanium在编译的时候，把这个当作它默认的主题文件。
如果你创建了一个文件叫作theme.xml，这个新建的文件就会覆盖Titanium
默认的theme文件，并且会破坏编译。添加一个使用nine-patch的图片的
windowBackground添加到自定义主题里。

注意：把windowBackground items添加到这个主题的默认root activity即可。
如果你添加到别的主题中的话，这个图片可能无法显示。

platform/android/res/values/mytheme.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
<style name="Theme.MyTheme" parent="Theme.AppCompat">
    <item name="windowBackground">@drawable/background</item>
    <item name="android:windowBackground">@drawable/background</item>
</style>
</resources>
```

- 生成`build/android/Androidmanifest.xml`之后，编译。打开这个文件可以看到
<activity>标签内包含着你默认的root activity，<android:name attribute>
中包含着你应用的名字：

build/android/AndroidManifest.xml:

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

- 复制默认的root activity到tiapp.xml中的Android部分的<application>中，
我们需要在<android>标签对中添加<manifest>和<application>标签，
在这个activity的`android:theme`属性中用我们自定义主题的名字替换掉Theme.

tiapp.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<ti:app xmlns:ti="http://ti.appcelerator.org">
    ...
    <android xmlns:android="http://schemas.android.com/apk/res/android">
        <manifest>
            <application>
                <activity android:name=".YourapplicationnameActivity"
                    android:label="@string/app_name"
                    android:theme="@style/Theme.MyTheme"
                    android:configChanges="keyboardHidden|orientation|screenSize">
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

创建一个新的应用时，Android会使用名字叫`default.png`的文件作为启动图。
你设置的图片文件的大小，尺寸和目标设备的屏幕差别很大。

在Resources/android/images文件夹中，有很多类似于`res-long-land-hdpi`的文件夹。

Titanium提供默认的，合适的启动图，放在Resources/android/images下的各个目录下。

如果你不想做各种特定尺寸的适配的话，你可以删掉那些文件夹。
然后只把一个default.png文件放在Resources文件夹下。

但是要注意的是：结果可能是在某个设备上，启动图开起来是拉伸或者压缩的。

注意：不要用`<supports-screens/>`元素和任何`android:anyDesity`
属性来设置不支持多屏幕适配。Google不建议修改默认的值，否则有可能表现不正常。

## iOS 图片的要求

iOS中的各种图片和Android有很多不同。

所有的图片都必须是PNG格式的，如果不是的话，都会被忽略掉。

对于使用了Alloy的项目，把图片们都放在`app/assets`，`app/assets/iphone`或者
`app/assets/ios`文件夹下。

如果是经典模式下的Titanium项目，把文件放在`Resources`，`Resources/iphone`，
`Resources/ios`文件夹下。

对于所有的icon文件（文件前缀叫appicon的），这些图片是需要是正方形。

如果某个Titanium项目缺少icon文件，编译就会失败。

对于用来编译的图片文件（图片文件前缀是Default的）则不会对编译造成影响。

