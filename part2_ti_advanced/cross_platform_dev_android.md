Welcome to Android World!!!

# Android开发
使用Titanium开发mobile app，虽然Titanium尽量abstract不同移动OS(Android，iOS)之间的差异，
但是不同平台还是有一些特定于自己平台的东西，需要在实际的开发中注意。

## Android应用开发注意事项
- Android有实体按键，这在实际的开发当中需要考虑。
- Android是一个开源的操作系统（open source），不同厂商厂商的Android设备差异巨大。Android的UI规范不具有强制性，仅仅是一个建议。
- 还有一点非常重要，就是各家OEM厂商生产的的Android的设别的分辨率差异巨大。

## Android的实体按键
- Back
- Home
- Menu
- Search

## 原生的Android开发知识
Android的app有四部分组成
- Activities
- Services
- Content Providers
- Broadcast receivers

### Activities
在Android的世界里，一个activity可以简单的认为是一个single screen，普通的screen就是不同的activity。
比如一个Android手机上的email客户端，邮件列表的screen是一个activity，写邮件的screen是另一个screen。

这里的关键点在于，在Android里，所有的activity都是separated。具体的表现就是，你在使用微信的时候，可以
使用相机或者录像的功能，还有比如说微信的扫一扫功能，都是调用了手机上的其他app的activity。

值得注意的是，Android的app也是sandbox机制，一个app如果调用另一个app的activity，被调用的activity其实跑在另一个进程里面。

### Services
Service，简单的可以理解成为跑在background的一个服务，不提供图形界面，并且不影响用户操作手机上的其他部件。

比如，可以在后台提供下载数据等服务。

### Content Providers
Content Provider是内容管理器。比如，在安装某个Android app，或者app的使用过程中，会提示你，是否允许这款app访问你的通讯录，
这里，其实是在设定这个app是否有权限去读或者写通讯录的Content Provider提供的内容。

### Broadcast receivers
Broadcast receiver，广播接收者。

每一个app都会有一个Broadcast receiver，比如说，当电池的电量过低，屏幕与trun off, 或者刚刚拍了一张照片的时候，Android这个OS会广播这条信息给所有的app知道。

或者说系统下载了某些数据，然后通知所有其他的可以使用这些数据的app知道，来使用这些数据。
