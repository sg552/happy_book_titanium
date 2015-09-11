Welcome to Application Structure World!

## Titanium应用的整体结构
下面通过mobile phone跟web的对比，进行说明。

### Window vs Web Page
### View vs Div

大致包括以下几个方面:
- 手机端的Window等同于web中的一个页面(web page)
- 手机端的View等同于web中的div
- Window是顶层容器，用来包裹其他的view
- View用来包裹各种基本的UI，比如Button，imageView，ScrollView，以及View本身
- 大部分情况下，Window跑在自己的context上，而使用tabGroup，可以让多个window并存
- Android和iOS，都可以使用open()和close()打开和关闭一个Window
- 打开的Window会放在Window stack的最顶层
