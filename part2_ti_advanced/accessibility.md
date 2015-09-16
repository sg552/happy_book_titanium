# Titanium中accessibility的使用

简介:1.设计一般的可访问的程序 2.语音反馈功能的特点

这个课题是一个使用语音反馈的使用了android和ios的辅助设备，设计了一个可访问的应用程序。

语音反馈功能:Android和iOS的画外音对讲为Android和iOS设备的视障人士的辅助功能，分别。这两个功能提供口头反馈给用户来描述他们是什么，他们是触摸，选择，激活等。
在Android平台上，对讲不同的Android版本。支持的视图元素和用户界面在安卓版本之间变化。用户可能需要从谷歌下载对讲早期的Android设备播放。对讲Android 4.1及以后的使用类似于iOS VoiceOver手势。
在iOS平台，画外音可在iOS 3。x和后。
支持两个口语反馈助理，所有钛视图元素支持一组的可访问性属性（见表如下），它可以用来指定文本发言的用户界面元素。这些视图中的许多元素都有一个默认值，该值是基于控制类型，并且可能已经被视觉障碍用户访问。设置这些属性可能不需要为您的应用程序。如果您的应用程序中有非文本元素，则是以图形方式提供信息，例如星评系统，您需要显式地将这些属性设置为有帮助的提示、标签和值，这样它们就可以传递相同的信息并可访问
Android与iOS的外音对讲行为
Android和iOS的外音对讲不同的表现与导航和语音反馈。以下面的代码为例：

```javascript
var win = Ti.UI.createWindow({
      title: 'Welcome',
      layout: 'vertical',
      backgroundColor: 'white'
});
var win2 = Ti.UI.createWindow({
      layout: 'vertical',
      left: '25dp',
      top: '25dp',
      width: '100dp',
      height: '100dp',
      backgroundColor: 'red',
      zIndex: 1,
});
var button2 = Ti.UI.createButton({
      title: 'Red',
      accessibilityLabel: 'Double-click me to close the red window'
});
button2.addEventListener('click', function(){
     win2.close();
    });
var label2 = Ti.UI.createLabel({
    text: 'Salut, Monde!',
    font: {fontSize: '24dp'},
    accessibilityHint: 'I do not speak French.'
});
win2.add(label2);
win2.add(button2);
var win3 = Ti.UI.createWindow({
   layout: 'vertical',
   bottom: '25dp',
   right: '25dp',
   width: '100dp',
   height: '100dp',
   backgroundColor: 'blue',
   zIndex: 3,
   accessibilityHint: 'I am a blue window'
});
var button3 = Ti.UI.createButton({
   title: 'Blue',
   accessibilityHint: 'Close the blue window.'
});
button3.addEventListener('click', function(){
    win3.close();
    });
var label3 = Ti.UI.createLabel({
   text: 'Hello, World!',
   font: {fontSize: '24dp'},
   accessibilityLabel: 'You pushed me',
   accessibilityValue: 'Nominal',
   accessibilityHint: 'I am a label'
});
win3.add(label3);
win3.add(button3);
var slider = Ti.UI.createSlider({
   min: 0,
   max: 100,
   width: '100%',
   value: 50
});
var button = Ti.UI.createButton({
   title: 'Open'
});
button.addEventListener('click', function() {
    win2.open();
    win3.open();
    });
var label = Ti.UI.createLabel({
    text: 'I pity the foo.',
    font: {fontSize: '24dp'}
})
win.add(button);
win.add(slider);
win.add(label);
win.open();
```
最初，应用程序显示一个白色的窗口有一个按钮，滑块和标签。在这一点上的用户体验，都表现出同样的对讲和外音。由于无障碍属性的定义，无论是口头反馈助理提供默认反馈。看到每个元素的口头答复表。
当您双击使用打开按钮时，应用程序会显示左上方的红色窗口和右下方的蓝色窗口。在这一点上的用户体验，对讲和外音表现不同。
由于Win32，蓝色的窗口，在UI层次结构的顶层容器，画外音只为这种观点提供了容器的反馈。背景中的所有其他视图元素被禁用的画外音。用户不能与“红色”窗口或“白色”父窗口进行交互。然而，对讲还提供反馈和不禁用用户互动与任何可见的元素。
由于accessibilityhint定义形式等，蓝色的窗口，画外音不提供口头反馈给孩子们看的元素，唯一的窗口，但对讲提供所有元件的反馈以及窗口。此外，所有的孩子都认为元素是由外音禁用或无法访问，所以用户不能双击按钮关闭窗口，被困在这个应用程序状态
