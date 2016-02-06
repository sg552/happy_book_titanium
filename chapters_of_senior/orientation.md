#Orientation(屏幕方向)
在这个章节，我们要学习一下如何在Titanium中处理设备的屏幕方向。主要有如下几种情况。

+ 整个App在使用期间方向都是被锁定的。
+ 只在一个给定的Window中锁定方向。
+ 根据情况来改变屏幕方向。

在这我们开始做这个之前，我们需要先知道关于Android的一些特殊和微妙之处。在Android中要知道，你得到的屏幕方向不符合你设定的。你能设置的UI方向有这四种：protrait upright,landscape right,portrait upside-down,landscape left。但是当你真的去请求设置当前方向时，你只能在portrait 和 landscape中选择。官方说这是Android的特征，不是Titanium的问题。

还有一个特征需要注意到的是portrait (竖屏)和landscape (横屏)在手机和平板上是有差异的。在手机上，当顶部的角度为零（物理按键在下方）的时候，叫做竖屏；当顶部的角度为270度的时候，叫做横屏。在平板上，以传感器为对照，当顶部角度为0的时候，叫横屏；当顶部角度为90度的时候，叫做竖屏。在开发的时候，这些是需要注意的。

##Orientation design principles（设计原理）
苹果开发文档说：“用户希望从不同方向体验你的app，所以你最好是能够满足他们的这种期望”。所以，我们不要把处理orientation当作一个麻烦，要把它当作一个机会，一个让自己app变的更棒的机会。
苹果提醒大家在选择固定方向和允许变化方向时，一定要考虑下面这些原则：

+ 在iPhone和iPod Touch上，不要在一个单独的应用里混合使用锁定旋转和支持旋转。要么选择锁定，要么选择支持旋转。

+ 在iPhone上，不支持portrait-upside-down(竖着倒过来)，因为不能让用户在打电话的时候竖着倒过来使用。

+ 在iPad上，你要能够允许用户从任何方向使用你的App。

这些原理在Android上也是一样。

与其在把处理orientation当作一个要面对的‘necessary evil(必然的邪恶)’的话，不如把它当作一次机会。当用户翻转他的设备的时候，你可以给他展示不同的内容。比如一个食谱App，当他竖屏使用的时候，显示一个食材菜单，当他横屏使用的时候，却给他显示一个菜谱。有些听筒的在电话被倒过来的时候，会有弱化，这时候你就需要考虑在你的App中来应对这种方向上的变化。

##如何限制你的App orientation mode
你可以在你的项目的`tiapp.xml`文件中设置你的orientations。这是设置splash screen的方向的方法，而且这会限制你的应用进来的时候的一些window，但不必设置到一些特殊的window上。
iOS和Android是有差异的，所以我们分开讨论。

###iOS
我们需要在tiapp.xml中用`UISupportedInterfaceOrientations`这个key来设置orientation modes。Titanium 默认设置iPhone支持垂直倒立方向，iPad支持任意方向。

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

###Android
Android可以使用同样的方法在tiapp.xml中设置，也可以用别的方法。Android中最重要的配置文件就是`AndroidManifest.xml`。在编译的时候，你写在tiapp.xml里的那些配置都会在打包你的app的时候生成Android Mainifest。如果要强行设置orientation的话，你就需要要把生成的Android Manifest文件里的内容copy到tiapp.xml，并且修改它们再重新编译。

+ 在Titanium中编译你的App

+ 打开tiapp.xml文件

+ 接下来你就要开始修改它：
 + 找到这行`<android xmlns:android="http://schemas.android.com/apk/res/android"/>`，把最后的那个反斜杠删掉

 + 然后添加一个闭合标签`</android>`

 + 在<android></android>之间添加一对标签`<manifest></manifest>`

 + 打开你项目下的`/build/android/AndroidManifest.xml`文件

 + 拷贝`<application>`标签对里的所有`<activity>`标签对里的内容。例如下面：

 AndroidManifest.xml
 ```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android" package="com.myapp.app" android:versionCode="1" android:versionName="1.0">
  <uses-sdk android:minSdkVersion="10" android:targetSdkVersion="19"/>

    <!-- Start Copying Here -->

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

    <!-- Stop Copying Here -->
  <uses-permission android:name="android.permission.INTERNET"/>
  <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
  <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
  <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
  <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
  <uses-permission android:name="android.permission.ACCESS_MOCK_LOCATION"/>
</manifest>
 ```

 + 把`<manifest></manifest>`标签对粘贴到你的tiapp.xml中。从此以后，每一次你编译你的应用的时候，Titanium都会拷贝那些activity标签对到生成的Android Manifest 文件，你已经设置好了你的UI orientation。

 + 想设置你想要的方向，就在每一个activity标签上加上`android:screenOrientation`属性。最后你的tiapp.xml中的manifest项应该看起来像下面这样：

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

##如何限制你的App 中某个window的orientation mode
当你不想把一个关于orientation的设置应用到整个App的所有window，只想应用到某个window上，又或者想让A window横屏，B window竖屏。那该怎么办呢？接着往下看。
你可以设置window的`orientationModes`参数，你可以通过这个参数使用一个UI组件数组来设置它的可以变化的方向。

###iOS上要注意的
要强制通过`orientationModes`来设置一个不具备变化方向的window能变化方向，这是非常糟糕的，也不会实现的。我们可以使用NavigationWindow 或者TabGroup。

```javascript
var win = Ti.UI.createWindow({
  /* on Android, it needs to be a "heavyweight" window */
  fullscreen: false,
  /* This works on iOS */
  orientationModes: [
    Ti.UI.PORTRAIT,
    Ti.UI.UPSIDE_PORTRAIT
  ]
});
// but for Android using Titanium prior to 2.1 you have to set it after creation
win.orientationModes = [Ti.UI.PORTRAIT, Ti.UI.UPSIDE_PORTRAIT]
```

##如何应对orientation的变化
还有很重要的一点就是，当你App UI的方向变了，你要来改变，刷新你的UI，比如按钮，图片之类的。
```javascript
Ti.Gesture.addEventListener('orientationchange',function(e) {
  // get current device orientation from
  // Titanium.Gesture.orientation
  // get orientation from event object
  // from e.orientation
  // Ti.Gesture.orientation should match e.orientation
  // but iOS and Android will report different values
  // two helper methods return a Boolean
  // e.source.isPortrait()
  // e.source.isLandscape()
});

```
##启动图如何设置方向
默认Titanium会加载一个默认的启动图，你是可以进行修改的，但不能完全的删除启动图。
###Android
+ 文件名字必须是default.png，其中d要小写。由于平台特殊性，这个文件一如既往的放在了你项目的`Resources/android`目录下。

+ 你可以根据你安卓设备的像素，方向等来设置你的启动图。因为和Android 的image规则是一样的。

###iOS
+ 文件名字必须是Default.png，其中D要小写。由于平台特殊性，这个文件一如既往的放在了你项目的`Resources/iphone`目录下。

+ 你可以提供一个视网膜版本的启动图，但必须取名叫做`Default@2x.png`。

+ 对于iPad和普遍的app，你都要提供`Default-Landscape.png`和`Default-Portrait.png`来做它的启动图。

