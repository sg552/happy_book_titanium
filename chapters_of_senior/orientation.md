# 屏幕的旋转

主要有如下几种情况。

- 整个App在使用期间方向都是被锁定的。
- 只在一个给定的Window中锁定方向。
- 根据情况来改变屏幕方向。

在这我们开始做这个之前，我们需要先知道关于Android的一些特殊和微妙之处。
在Android中要知道，你得到的屏幕方向不符合你设定的。

你能设置的UI方向有这四种：

- protrait upright 竖直朝上
- landscape right 水平向右
- portrait upside-down 竖直朝下
- landscape left 水平向左

但是当你真的去请求设置当前方向时，你只能在portrait 和 landscape中选择。
这是Android的特性，不是Titanium的问题。

还有一个特性, portrait (竖屏)和landscape (横屏)在手机和平板上是有差异的。

在手机上，当顶部的角度为零（物理按键在下方）的时候，叫做竖屏；
当顶部的角度为270度的时候，叫做横屏。

在平板上，以传感器为对照，当顶部角度为0的时候，叫横屏；
当顶部角度为90度的时候，叫做竖屏。

在开发的时候，这些是需要注意的。

## 如何限制app的屏幕不变化？

你可以在你的项目的`tiapp.xml`文件中设置你的orientations。这是设置splash screen的方向的方法，而且这会限制你的应用进来的时候的一些window，但不必设置到一些特殊的window上。
iOS和Android是有差异的，所以我们分开讨论。

### iOS

在tiapp.xml中用`UISupportedInterfaceOrientations`来设置orientation modes。

Titanium 默认设置iPhone支持垂直倒立方向，iPad支持任意方向。

`tiapp.xml`
```xml
<?xml version="1.0" encoding="UTF-8"?>
<ti:app xmlns:ti="http://ti.appcelerator.org">
    <ios>
        <plist>
            <dict>
                <key>UISupportedInterfaceOrientations~iphone</key>
                <array>
                    <string>UIInterfaceOrientationPortrait</string>
                </array>
                <key>UISupportedInterfaceOrientations~ipad</key>
                <array>
                    <string>UIInterfaceOrientationPortrait</string>
                    <string>UIInterfaceOrientationPortraitUpsideDown</string>
                    <string>UIInterfaceOrientationLandscapeLeft</string>
                    <string>UIInterfaceOrientationLandscapeRight</string>
                </array>
            </dict>
        </plist>
    </ios>
</ti:app>
```

### Android

Android中最重要的配置文件就是`AndroidManifest.xml`。
如果要强行设置orientation的话，你就需要要把生成的Android Manifest
文件里的内容copy到tiapp.xml，并且修改它们再重新编译。

- 在Titanium中编译你的App
- 打开tiapp.xml文件
- 接下来你就要开始修改它：
  - 找到这行`<android xmlns:android="http://schemas.android.com/apk/res/android"/>`，把最后的那个反斜杠删掉
  - 然后添加一个闭合标签`</android>`
  - 在<android></android>之间添加一对标签`<manifest></manifest>`
  - 打开你项目下的`/build/android/AndroidManifest.xml`文件
  - 拷贝`<application>`标签对里的所有`<activity>`标签对里的内容。例如下面：

 AndroidManifest.xml
 ```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android" package="com.myapp.app" android:versionCode="1" android:versionName="1.0">
  <uses-sdk android:minSdkVersion="10" android:targetSdkVersion="19"/>

  <!-- 从这里开始复制 -->
  <application android:icon="@drawabe/appicon" android:label="MyApp" android:name="MyappApplication" android:debuggable="false" android:theme="@style/Theme.AppCompat">
    <activity android:name=".MyappActivity" android:label"@string/app_name" android:theme="@style/Theme.Titanium" android:configChanges="keyboardHidden|orientation|screenSize">
      <intent-filter>
        <action android:name="android.intent.action.MAIN"/>
        <category android:name="android.intent.category.LAUNCHER"/>
      </intent-filter>
    </activity>
    <activity android:name="org.appcelerator.titanium.TiActivity" android:configChanges="keyboardHidden|orientation|screenSize"/>
    <activity android:name="org.appcelerator.tianium.TiTranslucentActivity" android:configChanges="keyboardHidden|orientation|screenSize" android:theme="@style/Theme.AppCompat.Translucent"/>
    <activity android:name="ti.modules.titanium.ui.android.TiPreferencesActivity" android:configChanges="screenSize"/>
  </application>
  <!-- 从这里结束复制 -->
</manifest>
 ```
  - 把`<manifest></manifest>`标签对粘贴到tiapp.xml中。
  从此以后，每一次你编译你的应用的时候，Titanium都会拷贝那些activity
  标签对到生成的Android Manifest 文件，你已经设置好了你的UI orientation。

  - 想设置你想要的方向，就在每一个activity标签上加上`android:screenOrientation`
  属性。最后你的tiapp.xml中的manifest项应该看起来像下面这样：

 tiapp.xml
 ```xml
<?xml version="1.0" encoding="UTF-8"?>
<ti:app xmlns:ti="http://ti.appcelerator.org">
    <android xmlns:android="http://schemas.android.com/apk/res/android"/>
      <manifest>
      <application android:icon="@drawable/appicon"
                         android:label="MyApp"
                         android:name="MyappApplication"
                         android:debuggable="false"
                         android:theme="@style/Theme.AppCompat">
        <activity android:screenOrientation="nosensor"
                          android:name=".MyappActivity"
                          android:label="@string/app_name"
                          android:theme="@style/Theme.Titanium"
                          android:configChanges="keyboardHidden|orientation|screenSize">
          <intent-filter>
            <action android:name="android.intent.action.MAIN"/>
            <category android:name="android.intent.category.LAUNCHER"/>
          </intent-filter>
        </activity>
        <activity android:screenOrientation="nosensor"
                          android:name="org.appcelerator.titanium.TiActivity"
                          android:configChanges="keyboardHidden|orientation|screenSize"/>
        <activity android:screenOrientation="nosensor"
                          android:name="org.appcelerator.titanium.TiTranslucentActivity"
                          android:configChanges="keyboardHidden|orientation|screenSize"
                          android:theme="@style/Theme.AppCompat.Translucent"/>
        <activity android:screenOrientation="nosensor"
                          android:name="ti.modules.titanium.ui.android.TiPreferencesActivity"
                          android:configChanges="screenSize"/>
      </application>
    </manifest>
  </android>
</ti:app>
 ```
