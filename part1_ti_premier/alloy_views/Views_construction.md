###View的结构组成。
在编写Alloy 的UI时，我们有三种实现方式。只写XML文件，把UI布局和组件样式都写在XML文件中；或者，在XML文件中写布局文件，在TSS文件中写样式文件；当然，还可以在XML写布局，部分特定的样式也写在XML中，公共样式写在TSS文件中。和HTML与CSS的方式类似，我们在写UI布局的时候可以给元素定义id和class，然后在样式中对具有相同class的元素写公共的样式。

####属性字段
Alloy View中可以使用属性字段：id、class、autoStyle、formFactor、if、module、ns、platform.

```
id:在每个view中是唯一存在的，在controller中可以通过$.id_name调用定义的元素。在style中通过“#id_name”表示。不同的View可以有相同的id。
class:给具有某些相同特性的元素定义标识。在style中通过“.class_name”表示。
platform:判断这个元素使用的平台，ios、android等。
formFactor:判断设备尺寸大小，手持类还是平板类。
if:自定义条件判断语句。
module:引用一个CommonJSmoudle。
ns:指定元素的namespace，对Ti.UI做重载。
```

#####platform
在判定使用的平台时，我们使用platform字段，platform='ios',表示适用ios平台。多个平台使用逗号隔开,如: platform='ios,android'。还可以使用‘!’表示否定状态，如: platform='!ios',表示除了ios外的其他平台。
#####formFactor
formFactor用来判定设备的尺寸大小，只具有两个属性值:handheld和tablet，分别表示手持设备（Phone,PDA等）和平板设备。
#####namespace
在View中我们对Ti.UI为命名空间的组件可以直接使用组件名作为标签名，但是如果要再view中使用其他非Ti.UI为命名空间的UI组件我们可以使用ns字段实现。
```
<View ns='Ti.Map' id='map_view'>
```
如上，定义了一个Ti.Map.View的组件，标签名直接使用View，由于会和Ti.UI.View冲突，所以使用ns字段指定其命名空间。
Ti是Titanium的缩写。Titanium.UI.View = Ti.UI.View
